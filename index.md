---
layout: exercises
title: Intro Android Exercises
---

## Intro Android Exercises

The goal of this project is to complete a series of exercises that are designed to reinforce our Android concepts. This project is appropriate for someone just starting out with Android development and is following along with the CodePath Android curriculum.

TODO: More information on the exercises

### Getting Started

Let's create an Android project that we can use to complete our exercises!

**Goal**: Create a new Android project

**Description**

Welcome to Android development!  We're going to explore Android concepts by following the various instructions in these text files.  In this first step, we will create the Android project that we will use for the rest of these exercises.

The "New Project" wizard will contain options not specified below.  Unless the directions below say otherwise, you may accept the default options.

**Directions**:

1. Open Eclipse, and select File->New->Android Application Project
2. Choose an application name, as you want it to appear when it is installed on a phone.
  - Note: It's ok to keep the default com.example prefix for now.
  - In the future you might want to use a more accurate namespace.
3. Set your minimum required SDK to 10.
4. When you create the Activity, you should use the default template, a Blank Activity.
4. Run your application
   - It should launch in the emulator
   - Should display "Hello World" on a white screen.
5. You're done!

#### Choosing SDK versions

Minimum required SDK: In the world, Android phones are running many different versions of Android. You need to select the minimum version that you will support. The lower the version, the more difficult it is to support because it will not have features of later versions. Unfortunately, many phones are unable to update their Android versions.

Use this site to help choose what the minimum required SDK version should be: http://developer.android.com/about/dashboards/index.html

As of right now, 45% of phones use API level 10. If you choose to only support API level 16, only 12% of phones will be able to install your application.

Target SDK should be set to the highest possible value. For new projects, it should match the "Compile With" property. This is an indication to the operating system that you've tested your application with a particular version. If the user upgrades their phone's OS past your indicated target SDK, the phone will run your app in a compatibility mode. `Compile With` should be set to the highest possible value.

## Screenshots

TODO: Exercise screenshots