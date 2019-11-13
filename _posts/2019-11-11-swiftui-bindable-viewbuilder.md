---
title: "SwiftUI - Bindable continued.."
date: 2019-11-11
categories:
  - blog
tags:
  - SwiftUI
  - View Builder
  - State
  - Bindable
---

<span style="font-size:12pt">Continuing on from a prior post on SwiftUI and Bindable State, I'll add a few declarative techniques for driving the display of views based on user action</span>

<span style="font-size:12pt">In the prior post I build a simple sign on screen where the login button enables only when something is entered into the password securetext field.</span>

In this post I'll demonstrate a common use case of showing the user the secure text password as clear text by tapping a button.  In addition an info banner will update
as well.  


![](https://cjazz.github.io/assets/images/BindableStatesPlus.gif)

There are 2 common ways of displaying different views based on actions in SwiftUI.
Each checks for a @State variable (binding) change.

In essence it'll be completely declarative for the first example and lower level using a ViewBuilder technique.

Declarative version:

```swift

if showPassword {
  ShowPasswordSecurityReminder<Text>()
} else {
   ShowInfoBanner<Text>()
}

```
View Builder version:

```swift
ViewBuilder.buildBlock(
  showPassword == true ?ViewBuilder.buildEither(first:ShowPasswordSecurityReminder<Text>()) : ViewBuilder.buildEither(second: ShowInfoBanner<Text>())
)
```

Nice to have two options, however I prefer Declarative in this context.

Full Xcode project can be retrieved [here](https://github.com/cjazz/SwiftUI-BindableStates)

**Happy Coding!**

![](https://cjazz.github.io/assets/images/clipartwiki.com-development-clipart-408069.png)
