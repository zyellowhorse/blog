---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: Things I Learned This Week 1
publishDate: 19 Dec 2021
name: Zac Yellowhorse
description: I spent a large portaion of my days working on getting an iOS app build and deploy working with Github Actions...

---
I spent a large portion of my days working on getting an iOS app build and deploy working with Github Actions also learning a few quarks along the way.

- [Github Actions does not support docker actions on Windows and MacOS runners](#first)
- [Github Actions runner specified version latest effectively means "stable" not latest](#second)
- [Apple Developer Enterprise Program Exists](#thrid)

<a name="first" ></a>
## Github Actions does not support docker actions on Windows and MacOS runners
When running the workflow for an iOS app running on macos-latest I ran into this error message:

> Container action is only supported on Linux

It seems self explanatory but wanted to make sure I just didn't do something incorrectly to get this error message so I did some googling which lead me to this [doc](https://docs.github.com/en/actions/creating-actions/about-custom-actions#types-of-actions). 

Basically it gave a little more context on the error message but yeah containerized actions will only work on linux runners at the moment. Luckily for me the actions I was trying to do had a cli for it so I just installed it as part of the pipeline and completed the task I need. 

<a name="second" ></a>
## Github Actions runner specified version latest effectively means "stable" not latest
When I was testing out the Github Actions pipeline the app would build and deploy correctly but when testers attempted to download the app and run it there would be a error saying: 

> Needs To Be Updated: The developer of this app needs to update it to work with this version of iPadOS.

The app was developed for 15.2 version of iOS and the tester's devices where on that version, as well as the applications project settings were set to that version so It was a little confusing. 

I looked up what versions of xcode and SDK packages were available on the macOS Github Actions and it showed that the 15.2 versions were [available](https://github.com/actions/virtual-environments/blob/main/images/macos/macos-11-Readme.md). The document I was reading was for macos-11 which everything looked correct and had the versions need to build that app. After some troubleshooting I found out that when I specified macos-latest in the github actions like so:
```yaml
jobs:
  Build:
    name: Deploy
    runs-on: macos-latest
```
"macos-latest" actually means stable because it was running my job as macos-10.15 while the latest was macos-11. It would have eventually switch macos-latest to being macos-11 but just a small thing that kept my build from working. The end result looked like this to get it working:
```yaml
jobs:
  Build:
    name: Deploy
    runs-on: macos-11
```

<a name="thrid" ></a>
## Apple Developer Enterprise Program Exists
Apple Developer Enterprise Program is a program that companies can join to get access to another distribution provisioning profile. Essentially it's a way to distribute customs apps for internal use only. The other way would be us to use an Adhoc provisioning profile that requires you to register the devices you wish to distribute the app to. With Enterprise provisioning profile you don't need to register the devices they just need to be in the same organization.

I learned about this from this [site](https://simplemdm.com/how-to-deploy-ios-apps-for-businesses/) when trying to get more information about provisioning profiles
