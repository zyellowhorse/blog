---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: How To Create Certificates for iOS Apps
publishDate: 24 Dec 2021
name: Zac Yellowhorse
description: Step by step on how to create certificates for iOS

---

I don't do this often enough to fully remember all the steps and have to look it up all the time. I might as well save the steps in a place I know where to look it up for future use if needed. 

.p12 files are used to publish app on the Apple App Store

### On your Mac Create a (.certSigningRequest) CSR file

1.  Open Keychain Access from Utilities
6.  Now from toolbar, open Keychain Access > Certificate Assistant > Request a Certificate From a Certificate Authority
7.  Enter email address that you used to register in the iOS Developer Program and common name
8.  Keep CA Email blank and select “Saved to disk” and “Let me specify key pair information”
9.  Click Continue
10.  Choose a filename & destination on your hard drive
11.  Click Save
12.  In the next window, set “Key Size” value to “2048 bits”
13.  Set “Algorithm” to “RSA”
14.  Click Continue

This will create and save your certSigningRequest file (CSR) to your hard drive. A public and private key will also be created in Keychain Access with the Common Name entered.

### Create ".cer" file in iOS developer account

1.  Login to apple developer account Click “Certificates, Identifiers & Profiles”
2.  Click "Provisioning Profiles"
3.  In the “Certificates” Click the “Add” (+) (Blue)
5.  Now, choose “App Store and Ad Hoc”
6.  Click Continue
7.  Click “Choose File” & find CSR file you’ve made from your hard drive
8.  Click Generate
9.  Click Download to get the file

### Install .cer and generate .p12 certificate

1.  Find .cer file you’ve downloaded and double-click
3.  Open up KeyChain Access and you'll find profile created in Step A
4.  You can expand “private key” profile (shows certificate you added) small arrow next to the certificate if under the "my certificates" tab
5.  Select only these two items (not the public key)
6.  Right click and click “Export 2 items…” from popup
7.  Now make sure file format is “.p12” and choose filename and destination on your hard drive. If ".p12" is grayed out that means you did not select the certificate and the private key 
8.  Click Save. Now, you’ll be prompted to set a password but keep these both blank
9.  It might prompt you for a password. At this point its asking for your admin password think sudo password 
10.  Click OK. Now, you have a .p12 file on your hard drive
