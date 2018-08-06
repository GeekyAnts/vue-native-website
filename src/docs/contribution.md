---
title: How to contribute
type: guide
order: 19
vue_version: 2.5.13
gz_size: "30.67"
---

## Open Development

All work on Vue Native happens directly on GitHub. Both core team members and external contributors send pull requests which go through the same review process.

## Your First Pull Request

Working on your first Pull Request? You can learn how from this free video series:
https://egghead.io/series/how-to-contribute-to-an-open-source-project-on-github

## Sending a Pull Request

The core team is monitoring for pull requests. We will review your pull request and either merge it, request changes to it, or close it with an explanation. We’ll do our best to provide updates and feedback throughout the process.

Before submitting a pull request, please make sure the following is done:

1.  Fork the repository `git clone git@github.com:GeekyAnts/vue-native-core.git` and create your branch from master.
2.  Run npm install in the repository root.
3.  Create a sample app using vue-native-cli separately outside the project repository.
4.  Within the project repository, go to packages folder `vue-native-core/packages`
5.  There are multiple modules which you can modify
    - vue-native-helper
    - vue-native-template-compiler
    - vue-native-core
6.  If you want modify the mobile app compiler. Then you would've to use vue-template-compiler or vue-native-helper based on your requirements. Update the build.js file accordingly.
7.  run `npm link <the-package-you-want-to-modify>`
8.  Format your code with prettier
9.  Run the app and test the code before you commit and create a pull request
