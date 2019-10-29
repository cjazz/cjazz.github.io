---
title: "SwiftUI - State and Binding"
date: 2019-10-28
categories:
  - blog
tags:
  - SwiftUI
---

With my prior post on Property Observers, I thought it apropos to demonstrate the same functionality with SwiftUI

Example - A login view controller where the login button is disabled until 
username and password are both entered.


Example:

```swift
struct ContentView: View {
    
    @State private var username = ""
    @State private var password = ""
    
    var body: some View {
        NavigationView{
            VStack {
                
                TextField("enter user name", text: $username)
                    .padding()
                SecureField("enter a password", text: $password)
                    .padding()
                
                HStack{
                    
                    Button(action: {}) {
                       Text("Login")
                        .background(buttonColor)
                        .foregroundColor(buttonTextColor)
                    }
                    .disabled(username.isEmpty || password.isEmpty)
                    .frame(minWidth: 0, maxWidth: .infinity)
                    .padding()
                    .foregroundColor(.white)
                    .background(buttonColor)
                    .cornerRadius(8)
                }
            }
            .font(Font.system(size: 28, design: .rounded))
            .textFieldStyle(RoundedBorderTextFieldStyle())
            .navigationBarTitle(Text("Login Form"))
            .padding()
            .font(.title)
            }
        }
    
    var userNamePasswordEntered: Bool {
        return !password.isEmpty && !username.isEmpty
    }
    var buttonColor: Color {
        return userNamePasswordEntered ? .blue : Color(.lightGray)
    }
    var buttonTextColor: Color {
        userNamePasswordEntered ? .white: Color(.secondaryLabel)
    }
}
```

Minus the additional adornments, SwiftUI is a bit less coding.  (I couldn't help myself)..

Example:

![](https://cjazz.github.io/assets/images/SwiftUI-state-binding.gif)


