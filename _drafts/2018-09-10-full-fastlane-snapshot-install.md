---
title: Using the "full" fastlane snapshot install
tags:
- fastlane
- ios
date: 2018-09-10 08:00:00
layout: post
---
There are two ways to install [`fastlane snapshot`](https://docs.fastlane.tools/getting-started/ios/screenshots/) in your project - a "standalone" way (`snapshot`-only), or as part of the [fastlane](https://docs.fastlane.tools) "suite" of products. The second is better, here's why...

## So-So: Snapshot-only
`fastlane snapshot init`

dumps your `Snapfile` and any associated files into the top level of your project. Some day, when you want to use more fastlane tools and a `Fastfile`, you’ll regret that all of the files are dumped into the project's top level.

## Better: Part of the fastlane suite
`fastlane init`

and then selecting the "Automate screenshots" option creates a `fastlane` subdirectory in your project. All of the files (including a `Fastfile`) are created in there. As you add more `fastlane` tools to your project (and you will!), they'll all live together there. Nice and centralized, with everything fastlane-related in the same directory as the `Fastfile`

## No matter what you do...
Move the generated `SnapshotHelper.swift` file into the appropriate target directory (probably `*UITests`) and include it from there.  Don't make your UI target’s compilation rely on source code in that fastlane directory. It will _work_, but it’s going to confuse someone, someday.
