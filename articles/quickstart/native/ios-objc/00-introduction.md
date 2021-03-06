---
title: Introduction
description: Brief introduction to the iOS Objective-C tutorials.
---

This multi-step quickstart guide will walk you through managing authentication in your iOS apps with Auth0.

## Sample Projects

Each tutorial in the series includes a link to its corresponding sample project, which demonstrates how to achieve the goal from the tutorial in question. You can check out all the samples [here](https://github.com/auth0-samples/auth0-ios-objc-sample/).

## Dependencies

Each tutorial will require you to use either [Lock](https://github.com/auth0/Lock.iOS-OSX) or the [Auth0.swift](https://github.com/auth0/Auth0.swift) toolkit, or both.

A brief overview:

- [**Lock**](https://github.com/auth0/Lock.iOS-OSX) is a widget that is easy to present in your app. It contains default templates (that can be a bit customized) for login with email/password, sign up, social providers integration, and also password recovery.
- [**Auth0.swift**](https://github.com/auth0/Auth0.swift) is a toolkit that lets you communicate neatly with many of the basic [Auth0 API](https://auth0.com/docs/api) functions.

These dependencies are already integrated in each sample project through [Cocoapods](https://cocoapods.org/). We have chosen to use an approach of not git-ignoring them in the samples repo; that way, you don't have to worry about running pod commands. Once you've cloned the repo, the samples are ready to be run!

It's recommended that, as a starting point for your project, you download the [seed project](#seed-project) described above, which already includes these dependencies.

Otherwise, if you're starting an empty project of your own, or if you want to add authentication to an existing project from yours, you have to make sure you install them:

#### Cocoapods

If you are using [Cocoapods](https://cocoapods.org/), add these lines to your `Podfile`:

```ruby
use_frameworks!
pod 'Lock', '~> 1.28'
pod 'Auth0', '~> 1.4'
```

Then, run `pod install`.

::: note
For further reference on Cocoapods, check [their official documentation](http://guides.cocoapods.org/using/getting-started.html).
:::

## Your First Steps

Make sure you complete these steps before going through any tutorial:

## 1. Create a Client

If you haven't already done so, create a new client application in your [Auth0 dashboard](${manage_url}/#/applications/${account.clientId}/settings) and choose **Native**.

![App Dashboard](/media/articles/angularjs/app_dashboard.png)

#### 2. Add your credentials

Add your credentials in `Auth0.plist`. You have to create that file if it doesn't already exist in your project:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>ClientId</key>
  <string>${account.clientId}</string>
  <key>Domain</key>
  <string>${account.namespace}</string>
</dict>
</plist>
```

#### 3. Configure your callback URLs

Go to your [Client Dashboard](${manage_url}/#/applications/${account.clientId}/settings/${account.clientId}/settings) and make sure that *Allowed Callback URLs* contains the following:

```shell
{YOUR_APP_BUNDLE_IDENTIFIER}://${account.domain}/ios/{YOUR_APP_BUNDLE_IDENTIFIER}/callback
```

In your application's `Info.plist` file, register your iOS Bundle Identifier as a custom scheme. To do so, open the `Info.plist` as source code, and add this chunk of code under the main `<dict>` entry:

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>None</string>
        <key>CFBundleURLName</key>
        <string>auth0</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>{YOUR_APP_BUNDLE_IDENTIFIER}</string>
        </array>
    </dict>
</array>
```

**You're all set up to start integrating Auth0 in your app!**

The tutorial guides contained in this section will teach you the different things you can do with it. It's recommendable that you follow them sequentially in order, as they are progressive and there is content that usually needs to be learned from previous tutorials.

Have fun!
