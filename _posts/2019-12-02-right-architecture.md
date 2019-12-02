---
layout: post
title: "How to pick the right architecture for your next project"
tags:
  - Swift Evolution
  - swift 5
  - tutorial
  - guide
  - ios
  - macOS
  - uikit
  - watchkit
  - tvos
  - watchos
  - guide
  - iphone
  - architecture
  - guide
  - apple
hero: https://dreamcraft.io/assets/img/articlesHeaders/architecture.png
overlay: orange
published: true
---
An architecture that works for one project might not work for another project. There are many different aspects to consider when you are looking when you pick one. But still, you can write a high-quality version of your app in any architecture, and it is only related to understanding the strong and weak parts of the selected architecture. 
 <!–-break-–>
 
As I was working on different apps with different architectures, I started to see things that could be better. The best way to figure which structure is the best fit is by trying. Why? Just because there are a lot of materials on the web that will try to sell you the one that is trendy or one that might be good with a specific framework like (**MVVM** and **Rx or Combine**). For example, a few years ago, I was impressed by **VIPER** architecture, and I used it for a few of my pet projects, and I was happy with it. And if you asked me at that time what I would recommend **VIPER** would be my answer.


## Sometimes a question worth more than an answer.

At Dreamcraft, before choosing the right architecture, we keep a few questions in mind:

## Who will work with that project?
When you are working alone, you can experiment with different architectures. But, when you work on a project that has two teams iOS and Android, it is helpful two have projects with the same architecture since you can always see how things are made on other platforms by simply opening the repo. And once those projects are built with the same architecture, you can easily navigate and find what are you looking for.

## What problem we are trying to solve?
 Is it hard to orientate in the app codebase, or almost impossible to cover it with the tests. The are many problems, but you should know which problems can solve the architecture that you choose. For example, having a structured architecture helps you easier find code that you are looking for, which will save you a lot of time.

## How easy will it be for them to maintain and onboard new people on that project?
Wherever you are an employee or a contractor during the onboarding on an existing project, the two questions may pop into your head: Who wrote this code, and what the hell does it do? For example, if you never worked with **RX or Combine with MVVM**, you might be in such situation.  To eliminate such problems pick the right architecture with that in mind

