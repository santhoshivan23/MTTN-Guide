# MTTN - Guide 

Hello Developers, we will be going through various tech stacks we use to build, develop and manage applications in MTTN. Primarly :- 

1. Flutter - Android App Development
2. Swift - iOS App Development 
3. React.JS - Front-end Development.
4. Node.JS and Python (Flask) - Backend Development. 

# Flutter 

### [![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Google-flutter-logo.png/120px-Google-flutter-logo.png)](https://en.wikipedia.org/wiki/Flutter_(software))

**Flutter** is an open-source UI software development kit created by Google. It is used to develop applications for Android, iOS, Windows, Mac, Linux, Google Fuchsia and the web.

## Installation

Before you go ahead with this we strongly recommend you download Teamviewer as your mentor can then help you remotely debug whatever issue you are facing.

> ### Windows
To setup Flutter on Windows, follow these [official guidelines](https://flutter.dev/docs/get-started/install)

> ### MacOS
To setup Flutter on MacOS, follow these [official guidelines](https://flutter.dev/docs/get-started/install)

> ### Linux
To setup Flutter on Linux, follow these [official guidelines](https://flutter.dev/docs/get-started/install)


## Flutter Doctor

Flutter comes up with an awesome command line utility to check if your machine is set up for local development. Flutter has ```Flutter Doctor``` command 

***
![Flutter Doctor](https://blog.codemagic.io/uploads/2019/05/image1.png)
***
*Flutter Doctor for Windows Doesn't need XCode. Refer to Installation above*

It help guide developers through setting up the local development environment for both iOS and Android. Flutter Doctor inspects which tools are installed on the local machine and which tools need to be configured. Once the Flutter Doctor command is happy, we can carry on creating a new Flutter app.

## Editor
So for your default editor , we recommend you guys to use **[VSCode](https://code.visualstudio.com/download)** , as its a lightweight IDE compared to Android Studio.

## Project Structure

Let’s first see what’s in the project generated by the Flutter framework:

***
![Flutter Default Code Overview](https://blog.codemagic.io/uploads/2019/05/image2.png)
***

- **lib/** - just as *pub* (Dart’s package manager), all the code will be here. All files which help you render the app will have a ```.dart``` extension
- **lib/main.dart** - In the ```main.dart``` file, you create widgets and develop Flutter apps as per your needs
- **pubspec.yaml** - stores a list of packages that are required to run the application, just like package.json does it. You should remember that in Flutter projects you cannot use pub directly, but instead, you will use the Flutter command: flutter pub get <package_name>. If using VSCode, pubspec.yaml page has a download button on the side which runs the above command for all packages you need
- **ios/ & android/** - the code specific for each platform, including app icons and settings where you set what permissions you’ll need for your application (like access to location, Bluetooth). So to switch app icons or to allow some special features like ARCore to run on your device, you need to changes specifics here.


## Adding assets to your application

First we need to make an assets folder and add the necessary images or fonts that we need to import

Then we need to add that assets under the pubsec.yaml


## Adding Packages 

If we need to add features to our application we need to use packages , for example we need to launch urls from our application then we can use this package.
[Url Launcher](https://pub.dev/packages/url_launcher)

First we need to add that package in our pubsec.yaml file 

Then we need to import that package in our code

```
import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';
```


## Widgets

Now that you have installed flutter and are beginning to develop, We want to introduce you to what exactly widgets are, in layman's term everything you use or interact with or even see on an app is a Widget.

Widget only one requirement: its method must returns other Widgets. The only exception to this rule are low-level widgets like 'Text' that return primitive types (Strings or numbers, usually.) 

This may sound intimidating at first, but you'll get along with the flow, Easiest way to visualize how Widgets work is to think of it as a complex tool with gears and levers and pulleys, basically built of simpler machines. When we build an app, we return a MaterialApp Widget which encloses other Widgets

```Dart
Widget build(BuildContext buildcontext){ //Here you return a Widget from the build function and the parameter it receives is a BuildContext object

return MaterialApp(                       // MaterialApp takes in a few parameters, as they are default parameters(Parameters with predefined values), if you wish to update any such parameter you explicitly mention the parameter and its value
      title: 'Welcome to Flutter',        // title here takes in a String input, hence "title : 'Welcome to Flutter'"
      home: Scaffold(                     // home takes in a Widget, for which we send a Scaffold Widget. Note: Scaffold holds all contents you'll be showing on your app
        appBar: AppBar(                   // appBar is a parameter of Scaffold which usually is provided with a Widget called AppBar. AppBar is the top bar you see in most apps which contain the menu and the search options
          title: Text('Hello World'),     // title again takes a Widget for which we provide a Text Widget. This provides for the title on the AppBar
        ),
        body: Center(                     // body contains the main content of your App which also takes in Widget 
          child: Container(
             child: Text('First App')
          )
        )
      )
 );
}
```

*If you ever wanna see what parameters are there for a specific widget press ```Ctrl+Space``` on VS-Code it shows you all the parameters for any Widget*

If you ever wanna know which Widgets to use refer to Flutter's [Widget Catalog](https://flutter.dev/docs/development/ui/widgets)

Flutter has its own youtube Channel as well which on which you can view videos for the Widgets you want to use.

Link : https://www.youtube.com/channel/UCwXdFgeE9KYzlDdR7TG9cMw


## Stateless and Stateful Widgets

Now we know how easy it is to use widgets. The next logical step would be to create our widgets. There are basically two kinds of widgets. They are called stateless and stateful widgets.

“Stateless” doesn’t mean they don’t have a state at all. Widgets is a Dart class, that can be declared with properties. But changing those properties in a stateless widget won’t affect what has already been rendered. Updating properties of a stateful widget will trigger life cycle hooks and render its content using the new state. We’ll start with Stateless widgets as they seem to be a bit easier.

### Stateless Widgets

To create one, we need:

1. A name for the new class
2. To extend our class from StatelessWidget.
3. Implement the build() method, that will receive one argument of type BuildContext and return a result of type Widget.

I have nothing more to add about Stateless widgets. They are simple.

> Refer to this [article](https://medium.com/flutter/how-to-create-stateless-widgets-6f33931d859) to know more

### Stateful Widgets

The following is the basic syntax of any Stateful Widget class.

```Dart
class MyApp extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return _MyAppState();
  }
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return Container(color: const Color(0xFFFFE306));
  }
}
```

So, here first, we have declared our main class called MyApp which extends the StatefulWidget class. That means now we have to define the generic method called ```createState()``` in that class which will return one another class which extends the generic class ```State```

> Refer to this [article](https://appdividend.com/2018/12/16/how-to-create-stateful-widget-in-flutter) to know more.

Let's understand the default flutter code.

# Import statements
This is where we import all the packages necessary for our flutter application.

```Dart
import 'package:flutter/material.dart';
```

# Main

This is just starting point of our application , here we are calling our root widget , this is just like int main() in C or public static void main() in Java

```Dart
void main() => runApp(MyApp());
```

# Root Widget

This is root widget of your application , **Title** property of the home page is being set as _Flutter Demo Home Page_ and under **Theme** we have color scheme as _blue_.

```Dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(   
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

# Home page 
This is the **Homepage** that will contain the body and other widgets in our application.

Here MyHomepage is a **statefulWidget** , which means the State of the homepage can be changed at anytime during the lifetime of our application, here we change the state when we click the button and increase the counter. 

```Dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);
  final String title;
  @override
  _MyHomePageState createState() => _MyHomePageState();
}
```

Lets look at different **components** on the homepage and see what they are doing.

The **onPressed** property will call the function which will increment our counter , and we add an icon on the button , by giving the icon to the child.

```Dart
floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
```

This function will increment the counter and **SetState** will update the the value of the counter , so that our application will reflect the changes.

```Dart
int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }
```

We will use the **Text Widget** to display the value of the counter , that will be updated everytime we click the button.

```Dart
children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.display1,
            ),
          ],
```
We encourage you guys to play around with the code , make some changes and see what happens.

Check out this [tutorial](https://www.youtube.com/watch?v=MNMtc7Bas-s) to learn more.

# Widget Tree

If all of this class-nesting is confusing, perhaps this visual of the ```Widget tree``` will help. This is what your current counter application looks like. 

# Sources to refer to:

## Flutter Widget Catalog:
Provides all the details about widgets available for UI development. It can be referred [here](https://flutter.dev/docs/development/ui/widgets).

## Cookbook:
This [cookbook](https://flutter.dev/docs/cookbook) contains recipes that demonstrate how to solve common problems while writing Flutter apps. Each recipe is self-contained and can be used as a reference to help you build up an application.

## Videos:
- Flutter Channel: https://www.youtube.com/channel/UCwXdFgeE9KYzlDdR7TG9cMw/about
- Tutorial by Smartherd: https://www.youtube.com/playlist?list=PLlxmoA0rQ-Lw6tAs2fGFuXGP13-dWdKsB


Here we will discuss about adding Assets to your project and using widgets to use these assets and build a functioning app

## Assets

**Flutter apps** can include both **code and assets** (sometimes called resources). An asset is a file that is bundled and deployed with your app, and is accessible at runtime. 

Common types of assets include static data (for example, JSON files), configuration files, icons, and images (JPEG, WebP, GIF, animated WebP/GIF, PNG, BMP, and WBMP).

Flutter uses the ```pubspec.yaml``` file, located at the root of your project, to identify assets required by an app.

```yaml
name: eventpagetask
description: Task 1

version: 1.0.0+1

environment:
  sdk: ">=2.1.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^0.1.2

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
  assets:            #Indentation is important while adding files
    - logo.png       #Files to be used as assets are provided here
    - oc.png
    - hawkeye.png
    - gambit.png
    - cicada.png 
```

## Steps to add and use Assets in your Project:

- Create ```assets``` folder in your project subdirectory
- Copy all images to be used as font into this directory
- Goto ```pubspec.yaml``` file in your project and make the necessary changes as shown above 
- Use the **Image Assets** in your program freely using Image.asset() 

> ```Dart
>
> ...
>    
>     return Container(
>        child: Image.asset('logo.png'),
>     );
>
>....
>
>```


## Commonly Used Widgets
***
## Container

For documentation click [here](https://api.flutter.dev/flutter/widgets/Container-class.html)...

A convenience widget that combines common positioning,containing and sizing widgets.

> A container first surrounds the child with padding (inflated by any borders present in the decoration) and then applies additional constraints to the padded extent (incorporating the width and height as constraints, if either is non-null). The container is then surrounded by additional empty space described from the margin.

> Containers with no children try to be as big as possible unless the incoming constraints are unbounded, in which case they try to be as small as possible. Containers with children size themselves to their children. The width, height, and constraints arguments to the constructor override this.

```Dart
Widget tile(...)
  {
      ...
      return Container(
        height: ...
        margin: ...
        decoration: BoxDecoration(
          shape: ...
          color: ...
          borderRadius: ...
        ),
        child: Row(children: 
          <Widget>[
             ...
             //Contains children Widgets for Row
             ...
          ],
        )
      );
}
```

## Column 

For documentation click [here](https://api.flutter.dev/flutter/widgets/Column-class.html)

Column Widget allows a user to arrange its contents vertically.

```Dart
import 'package:flutter/material.dart';

void main() => runApp(AppTask_1()); //The execution begins here where all the runApp being a function from the imported package executes a constructor of AppTask_1

class AppTask_1 extends StatelessWidget 
{
  @override
  Widget build(BuildContext context) 
  {
    return MaterialApp(
      title: ...
      home: EventPage(title: 'Page_Events'), // an object of EventPage class is sent as parameter for home
    );
  }
}

class EventPage extends StatefulWidget 
{
  EventPage({Key key, this.title}) : super(key: key);
  final String title;

  @override
  _EventPageState createState() => _EventPageState();
}

class _EventPageState extends State<EventPage> 
{
  
  Widget tile({String title,String logo,String date, String venue ,String time,BuildContext context})
  {
      ...
      ...
  }


  @override
  Widget build(BuildContext context) 
  {
    return Scaffold(
      appBar: AppBar(
        ...
        title: Text("IECSE Events"),
      ),
      body: Center(          //This center aligns whatever widget is provided to Center as child
        child: Column(       //Column Widget is used to arrange the different tiles vertically
            children: <Widget>[
            tile(...),
            ...
            ... //Call the tile method to return Containers which get distributed in Columns here
          ]
        ),
      ),
    );
  }
}

```

## Row 
For Documentation click [here](For documentation click [here](https://api.flutter.dev/flutter/widgets/Row-class.html)...

As we see Column distributes content vertically, Row is used for horizontal distribution of contents.

As you see in the example content is horizontally distributed in each tiles, so we need to use a Row Widget

```Dart
....

Widget tile({String title,...})
{
      Size size = MediaQuery.of(context).size; //Used to take dimensions of the device to make custom apps

      return Container(             //Tile is take as a container
        height: ... //Denotes height of each Tile
        margin: ... //Used for leaving empty space around the Container
        decoration: BoxDecoration(
            ... //Used to Add background, shape, colour gradient, or images to Container
        ),
        child: Row(children: 
          <Widget>[
            Container(
              width: ... //Provided with width of first component
              child: ... //Widget which the container will hold example Text(), Image.asset()
            ),
            Container(
              ...
            ),
            Container(
              ...
            )
          ],
        )
      );
  }
....
```

## Links

- [Use Rows And Columns - Medium](https://medium.com/jlouage/flutter-row-column-cheat-sheet-78c38d242041)
- [Container Cheat Sheet - Medium](https://medium.com/jlouage/container-de5b0d3ad184)
- [Functions in Dart - Dart.Dev](https://dart.dev/guides/language/language-tour#optional-parameters) 

# Swift 

## Swift Basics 

For Native iOS, we'll be using the programming language called Swift. First we need to go through the basics of the language before we begin making applications. 

### Topics to be read  : -
1. Basic Operators
2. Strings and Characters
3. Collection Types
4. Control Flow 
5. Functions
6. Structures and Classes

Read the topics [here.](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

## Xcode Basics 

Xcode is Apple's integrated development environment for macOS, used to develop software for macOS, iOS, iPadOS, watchOS, and tvOS. 

Xcode 12 has quite a lot of new features and changes. 
This tutorial will help you understand your way around it. 

Go through this [youtube video.](https://www.youtube.com/watch?v=MMoJiZZWoCA)









