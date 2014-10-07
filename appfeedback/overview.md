---
title: Overview
page_title: AppFeedback Overview
position: 1
---

# AppFeedback: Overview

With the <code>TKFeedbackController</code> implemented in your app you can gain invaluable insights into the users experience with it. Sending feedback on the users’ side is very easy. They can simply shake the device or navigate to the feedback option. The control takes a screenshot automatically and prompts the users to provide comments. The control is seamlessly integrated with Telerik Baas enabling developers to easily monitor and track all their users’ feedback in one place, rather than get it scattered across your mail, chat, spreadsheets or other ways of communicating with your users.

Telerik AppFeedback workflow is simple and easy:

- You use the TKFeedbackController component into your app. The component collects and displays feedback data the user sends.
- The AppFeedback project in your Telerik Platform workspace is a central repository that collects feedback items from the mobile apps running the Feedback component. The development teams use the project in the workspace to review and reply to the feedback items from users.

Features
===

To use Feedback component, you need to create a TKFeedbackController as a root UIViewController in your application and set the appliction root ViewControler as a content controller

```Objective-C
ViewController *mainViewController = [[ViewController alloc] initWithExample:[self createExamples]];
UINavigationController *navigationController = [[UINavigationController alloc] initWithRootViewController:mainViewController];
navigationController.navigationBar.translucent = NO;

TKFeedbackController *feedbackController = [[TKFeedbackController alloc] init];
feedbackController.dataSource = [[TKPlatformFeedbackSource alloc] initWithKey:@"58cb0070-f612-11e3-b9fc-1234567890" uid:@"developer@telerik.com"];
feedbackController.contentController = navigationController;

self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
self.window.rootViewController = feedbackController;
[self.window makeKeyAndVisible];
```
```Swift
let mainViewController = ViewController(example: self.createExamples())
let navigationController = UINavigationController(rootViewController: mainViewController)
navigationController.navigationBar.translucent = false
    
let feedbackController = TKFeedbackController()
feedbackController.dataSource = TKPlatformFeedbackSource (key: "58cb0070-f612-11e3-b9fc-1234567890", uid: "developer@telerik.com")
feedbackController.contentController = navigationController
    
self.window = UIWindow(frame: UIScreen.mainScreen().bounds)
self.window!.rootViewController = feedbackController
self.window!.makeKeyAndVisible()
```
```C#
ViewController mainViewController = new ViewController (this.CreateExamples());
UINavigationController navigationController = new UINavigationController (mainViewController);
navigationController.NavigationBar.Translucent = false;

TKFeedbackController feedbackController = new TKFeedbackController ();
feedbackController.DataSource = new TKPlatformFeedbackSource ("58cb0070-f612-11e3-b9fc-1234567890", "developer@telerik.com");
feedbackController.ContentController = navigationController;

this.Window = new UIWindow(UIScreen.MainScreen.Bounds)
this.View.Window.RootViewController = feedbackController;
this.View.Window.MakeKeyAndVisible ();
```


Once integrated, the Feedback component offers the following functionality from within the app running on the user’s device:

- It can take a screenshot of the user’s device current state.
- With the feedback sent by the end-user, the Feedback component can collect system data about what device, OS and application is used by the user (e.g. if it is iPhone or iPad, iOS version).
- It allows the user to enter a text description of their feedback. For example, a beta user might say, “Clicking the calendar icon causes the app to hang.” Together with the screenshot and device information, your team can make better evaluation of the feedback.
- It shows the feedback already sent, along with the current state for each feedback item (open or resolved).
- It shows the details about a given feedback item - the screenshot, the description, etc., sent from the device.

AppFeedback project in Telerik Platform
===

The AppFeedback project is where you and members of your development team receive and manage the feedback sent by your users. To access it, go to your Telerik Platform workspace and select the specific AppFeedback project.

There you can:

- See all feedback sent for that project
- Respond to feedback such as ask for more details, etc.
- Assign feedback items to workspace members on your team so you know who is responsible for handling the feedback
- Resolve feedback so you and your users know if the feedback has been implemented or resolved.
