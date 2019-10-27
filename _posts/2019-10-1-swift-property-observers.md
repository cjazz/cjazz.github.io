---
title: "Swift - Property Observers"
date: 2019-10-18T15:34:30-04:00
categories:
  - blog
tags:
  - Swift
---

The Swift language introduced in 2014 has grown and continues to evolve (open source).
As stated on the [About](https://swift.org/about/) page, one of it's goals is to make it easier to write code.   Having written Swift code for a number of years now, this is definitely the case.   

**Property Observers**
In the context of user interactivity, you can leverage Property Observers to 
control state based on values being set.  

Example - A login view controller where the login button is disabled until 
username and password are both entered.

```swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var userNameField: UITextField!
    @IBOutlet weak var passwordField: UITextField!
    
    @IBOutlet weak var loginButton: UIButton!
    
    var userName: String? {
        didSet{
            checkFields()
        }
    }
    
    var password: String? {
        didSet{
            checkFields()
        }
    }
    
    func checkFields (){
        guard let _ = userName else {return}
        guard let _ = password else { return }
        loginButton.isEnabled = true
        loginButton.backgroundColor = UIColor.systemBlue
    }
    @IBAction func enteredUserName(_ sender: UITextField) {
        userName = sender.text
        checkFields()
    }
    
    @IBAction func enteredPassword(_ sender: UITextField) {
        password = sender.text
        checkFields()
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        loginButton.isEnabled = false
        loginButton.backgroundColor = UIColor.lightGray
    }
}

```
Example:

![](https://cjazz.github.io/assets/images/ExampleLogin.jpg)

And there's more regarding Property Observers. Here's a good source for more: [NsHipster.com](https://nshipster.com/swift-property-observers/)



