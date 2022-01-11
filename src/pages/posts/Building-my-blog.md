---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: Building My Blog
publishDate: 23 Dec 2021
name: Zac Yellowhorse
description: This post is to document some of my though process and learning when it comes to building a personal blog site...

---

- [Intro](#intro)
- [Reason for creating a blog](#reason-for-creating-a-blog)
- [Choosing the tech stack](#choosing-the-tech-stack)
- [My approach](#my-approach)
- [Creating the site](#creating-the-site)
- [Deploying the site](#deploying-the-site)

## Intro
This post is to document some of my though process and learning when it comes to building a personal blog site. I have very little knowledge when it come frontend work because I have not put much time into it but I still want to learn more. I had a class on it in college but only towards the end of the class did they start to go over React but even then still don't remember much. I think this might be a good place to start when it comes building a website because its not the most difficult thing.

## Reason for creating a blog
I'm looking to build a blog so that I can have a place to document the things I am learning as be able to look back on subjects / projects. I have seen many postings mentioning blogging as a bonus. Being able to put your thoughts out there and being able to document your work is a plus. Even if this is not a contributing factor for a potential employer its a fun project to learn more frontend. 

## Choosing the tech stack 
I have already done some research on this and have decided that I am going to host the site on Netlify and build the site with Typescript using React and Astro.build. This blog is going to be a static site which is perfect for Netlify and Astro.build then going to use React for the UI elements. The only reason I know about Astro.build is because I follow Cassidoo on Twitch and she had mentioned it. I read into it and their [blog post](https://docs.astro.build/comparing-astro-vs-other-tools/) on Astro's performance vs other frameworks looked interesting even though I doubt I will run into performance issues. My other choice would have been to use Next.js because it seems to be popular. 

## My approach
I am going to start of by reading the documentation on Astro's site to see if there is any getting started information or examples. Once I feel like I have a decent understanding I am going to look at Cassidoo's blog post about build a blog which she used Next.js and React. I am probably going to be following that closely and switching out the Next.js stuff with the Astro equivalent. I found this [blog post](https://dev.to/cassidoo/build-wicked-fast-sites-with-astro-an-introduction-173j) that shows some features and details of Astro. There is some stuff in there that goes over my head but I'm not too worried about it. 

## Creating the site
I started out by using Astro's blog template. I created a new directory and ran `npm init astro` this gave me an option to select the blog template. I launched it immediately to see exactly what my base would look like. I had to install the dependencies and run the server with these commands: `npm install` and `npm run dev`. I was met with this screen: 
![Building_My_Blog_1](https://www.zacyellowhorse.com/posts_assets/Building_My_Blog_1.png)

Its a good place to start but the first thing I wanted to do was make put a dark theme on it. I forgot a lot about css but I after some googling I was able to figure out that I needed to edit the `src/styles/blog.css` file specifically the `:root` selector because that set the colors. I edited the `:root` to be `:root.theme-light` and changed the `:root.theme-dark` to be just `:root`. That gave me a dark theme.

I did a ton of these sort of changes in the css to get to a color scheme I like which eventually looked like this. 
![Building_My_Blog_2](https://www.zacyellowhorse.com/posts_assets/Building_My_Blog_2.png)

While I am not totally sold on the colors just yet I have something I can work with and be happy with for now. I did a ton of changes in the other files to get to something I like and got rid of the example data and images. I didn't use any React or Typescript to get to what I want as I most likely look into that later on. 

## Deploying the site
I chose to use Netlify to host my static site because I had used in the past for a different project. Astro has a section in their documentation that shows examples on how to deploy your site on different platforms [found here](https://docs.astro.build/guides/deploy/). I actually copied the steps here for the Netlify setup. Once my site was deployed with Netlify I setup my custom domain for it and I was all set.

I do plan on continuing to iterate on this site to improve readability and usability this was a great jumping off point. 
