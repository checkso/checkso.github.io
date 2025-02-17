---
title: How to Sideload Apps on an Amazon Kindle Kids Tablet
date: 2024-02-17
categories: [Amazon Kindle, App Sideloading, Parental Controls, Tech Hacks for Families]
tags: [YouTube Kids Installation, Kindle Kids Tablet Sideloading, Amazon Fire Tablet]
---


Amazon’s Kindle Kids Tablet offers a secure environment for children, but some apps like YouTube Kids aren’t preloaded. Here’s a parent-friendly guide to sideloading YT Kids (and in fact any other app) using Google Play Store and a third-party launcher.  

---

### **What You’ll Need**  
- The Kindle Kids Tablet 
- A computer with [ADB installed](https://www.xda-developers.com/install-adb-windows-macos-linux/)  
- A USB cable  

---

### **Step 1: Install Google Play Store (Parent Profile)**  
1. **Switch to the Parent Profile**: Enter your password to access parental settings.  
2. **Install Google Play Store**: Follow [this simplified guide](https://www.androidpolice.com/install-play-store-amazon-fire-tablet/) to download and install the Play Store via APK files.  
3. **Open the Play Store**, sign in with your Google account, and install **YouTube Kids**.  

---

### **Step 2: Install the App Launcher (Parent Profile)**  
1. Open the **Amazon Appstore** and search for **“App Launcher”** (yellow star on a blue background).  
2. Install it. To confirm the package name (e.g., `rocks.seufert.applauncher`), connect the tablet to your computer and run:  
   ```bash  
   adb shell pm list packages -3  
   ```  
   *This lists all third-party apps installed.*  

---

### **Step 3: Enable Developer Mode & ADB**  
1. On the tablet, go to **Settings > Device Options** and tap the **Serial Number** 7 times to enable Developer Options.  
2. Return to Settings, open **Developer Options**, and enable **USB Debugging**.  
3. Connect the tablet to your computer via USB. When prompted, check **“Always allow”** and tap **OK**.  

---

### **Step 4: Run ADB Commands (Child Profile)**  
1. **Switch to the Child Profile** on the tablet.  
2. **Find the Child Profile User ID** (usually `10`):  
   ```bash  
   adb shell pm list users  
   ```  
   *Look for the child profile’s ID (e.g., `UserInfo{10:Kids...}`).*  
3. On your computer, run these commands to link Google services to the child profile (**replace `10` if needed**):  
   ```bash  
   adb shell cmd package install-existing --user 10 com.google.android.apps.youtube.kids  
   adb shell cmd package install-existing --user 10 com.google.android.gms  
   adb shell cmd package install-existing --user 10 com.android.vending  
   adb shell cmd package install-existing --user 10 com.google.android.gsf  
   adb shell cmd package install-existing --user 10 com.google.android.gsf.login  
   ```  

---

### **Step 5: Allow App Launcher & Add YT Kids (Parent Profile)**  
1. **Switch back to the Parent Profile** and open **Settings > Parent Dashboard**.  
2. Go to **Child Profile > Allowed Apps** and ensure **App Launcher** is enabled.  

---

### **Step 6: Launch YouTube Kids (Child Profile)**  
1. **Switch to the Child Profile**.
2. **Open the App Launcher** on the parent profile, then:  
   - Tap the **Settings icon** (gear symbol) in the App Launcher.  
   - Select **YouTube Kids** from the list of installed apps.  
   - Save changes.   
3. The App is now visible with one click.

---

### **Troubleshooting Tips**  
- If YT Kids crashes, reboot the tablet.  
- Use `pm list packages -3` to verify installed apps.  
- Double-check user IDs with `pm list users` if commands fail.  

--- 

Enjoy a kid-friendly YouTube experience on your Kindle Tablet! 🚀
