---
title: Authorization
description: This tutorial will show you how assign roles to your users, and use those claims to authorize or deny a user to perform certain actions in the app.
---

<%= include('../../../_includes/_package', {
  org: 'auth0-samples',
  repo: 'auth0-ios-objc-sample',
  path: '07-Authorization',
  requirements: [
    'CocoaPods 1.1.1',
    'Version 8.2 (8C38)',
    'iPhone 6 - iOS 10.2 (14C89)'
  ]
}) %>

::: note
This tutorial assumes that you've already read the [rules tutorial](/quickstart/native/ios-objc/06-rules) and you know how to implement a basic rule in your app.
:::

### Before Starting

This tutorial assumes you are already familiar with Auth0 and how to Sign up and Sign in using Lock or Auth0 Toolkit. If you're not sure, check out [this tutorial](/quickstart/native/ios-objc/01-login) first.

Many identity providers will supply access claims, like roles or groups, with the user. You can request these in your token by setting `scope: openid roles` or `scope: openid groups`. However, not every identity provider provides this type of information. Fortunately, Auth0 has an alternative, which is to create a rule for assigning different roles to different users.

### 1. Create a Rule to Assigning Roles

First, you will create a rule that assigns your users either an `admin` role or a single `user` role. To do so, go to the [new rule page](${manage_url}/#/rules/new) and select the "*Set Roles to a User*" template, under *Access Control*. Then, replace this line from the default script:

```
if (user.email.indexOf('@example.com') > -1)
```

to match the condition that fits your needs. Notice that you can also set  roles other than `admin` and `user`, or customize the whole rule as you please.

By default, if the user email contains `@example.com` the user will be given an `admin` role, otherwise the user will be given a regular `user` role.

### 2. Test the Rule

To test the rule, use the following code snippet once you've gotten the user profile.

::: note
Check out the [login](/quickstart/native/ios-objc/01-login) and [user profile](/quickstart/native/ios-objc/04-user-profile) tutorials for more information on how to get the user profile.
:::

```objc
#import <Lock/Lock.h>
```

```objc
if([self.userProfile.appMetadata[@"roles"] containsObject:@"admin"]){
    //this user has admin access
} else {
    //this user does not have admin access
}
```

Notice that you'll find the `roles` information within the `appMetadata` dictionary from the `A0UserProfile` object. That's because of what's defined inside the rule.

### 3. Do Your Stuff

At this point, you are able to distinguish the users' roles in your app so you can authorize or deny access to a certain feature.

All you have to do here is to replace the commented out statements from the previous step with the instructions you need to execute depending on your business rules.

### Done!

That's it. You're already managing roles within your app, with a few simple steps.
