![[Screen Shot 2023-10-07 at 3.40.33 PM.png]]

- **Team**: later for uploading stuff in AppStore (same for Identifier)

- **Interface:
	- **SwiftUI**:
		- real-time preview
		- multicross between all Apple devices
	- **Storyboard**:
		- beneficial for already written code
		- outdated
-  --> **USE SwiftUI** 

- **Lifecycle:**
	- **SwiftUI App:**
		- "@main" entry point
		- Example:
	```
		import SwiftUI
		 
		 @main 
		 struct MySwiftUIApp: App 
		 { 
			var body: some Scene 
			{ 
				WindowGroup 
				{ 
					ContentView()
				} 
			} 
		 }
	```
	- **UIKit App Delegate:**
		- "UIApplicationDelegate" entry point
	- Lifecycle describes in witch state the Application will perform witch tasks and how active it is
	- both variants look very similar, different is just the declaration for entry point and function calls
	- just learn to use SwiftUI App lol
- --> **USE SwiftUI App**

- **How 2 start:**
	- **ContentView / SceneDelegate / AppDelegate:**
		- with SwiftUI as Interface and SwiftUI App as Lifecycle there a those options as starting points (entry points):
			- <span style="color: #d9c9ff; font-weight: bold;">ContentView.swift:</span>
			  ```
				import SwiftUI 
				
				@main 
				struct YourAppNameApp: App 
				{ 
					 var body: some Scene 
					 { 
						 WindowGroup 
						 { 
							 ContentView() 
						 } 
					 } 
				 } 
				 
				 struct ContentView: View 
				 { 
					 var body: some View 
					 { 
						 Text("Hello, World!") 
					 } 
				 }
		        ```
				-  default entry point
				- no access to AppDelegate or SceneDelegate methods (for advanced apps)
				- simple to handle for smol or middle big applications

			- <span style="color: #d9c9ff; font-weight: bold;">SceneDelegate.swift (iOS 13 and later):</span>
				- necessary if you're targeting iOS 13 and later because these versions of iOS use the scene architecture
				- multiple instances of your UI
				- good but overkill for beginners
	
			- <span style="color: #d9c9ff; font-weight: bold;">AppDelegate.swift (Optional for Advanced Customization):</span>
				-  Full control (deep linking, URL schemes, background fetch, and other system-level events)
				- for advanced shit -> guess not needed for beginner level
	- -->recommended is SceneDelegate.swift, but for first apps use **ContentView.swift** to learn the basics!

	- **whats a UIViewController?**
		- 




