---
layout: exercises
title: Chapter 10
---

## Chapter 10 - Publishing

### Exercise 1: Publishing

**Goal**: Generate an APK that can be used to publish to the Android Marketplace.

**Description**:

Publishing a completed app is fairly easy. It requires first signing the project and generating an APK.

**Directions**:

1. Self-sign the application using the signing wizard built-in to Eclipse.
   - Select File → Export → Android → Export Android Application
   - Verify project name and click Next
   - Select Create a new Keystore and pick any location and any password.
   - Type "DistributionKeyStoreAlias" as alias, enter 30 years of validity and name. Hit Next
   - Choose an APK file path and hit Finish
2. Publish the app (optional)
   - Visit http://market.android.com/publish/Home to register for a Google developer account (costs $25.
   - Enter information and complete the process
   - Click the Upload Application link to start the upload
   - Select APK file and upload screenshots and information
   - Enter app title, description, website, etc
   - Hit Publish to complete the uploading of your app.