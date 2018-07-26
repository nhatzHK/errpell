---
layout: post
title: "Making a button using QML and QtQuick"
category: guide
tags: programming
---

# Table of Contents

1.  [Introduction](#org1da39c4)
    1.  [GUI in C++, lul](#org36bff9a)
    2.  [What is QtQuick](#orge2d84f3)
2.  [First touch](#orga3206e3)
    1.  [Running qml code](#org920ef66)
        1.  [qmlscene](#orge115980)
        2.  [import](#org374a58c)
        3.  [qml file structure](#org5913eef)
    2.  [id and properties](#org0d0de08)
    3.  [Nesting](#org791864a)
    4.  [Children and parents](#org6b21b1b)
    5.  [Reactive programming or property binding](#org3e524f8)
3.  [Stuff & co.](#org453cbe4)
    1.  [Adding custom properties](#org836548e)
    2.  [signals](#org598628c)
    3.  [Anchors](#orgead4612)
    4.  [MouseArea](#org546fa81)
4.  [Combine all the things](#org32b8cc9)
    1.  [Beyonce](#org54e4c6d)
    2.  [Additional information](#org307b60f)
    3.  [Solution](#orgcdd9e47)

First published [here](https://programming.im/guides/16) on July 8, 2018.


<a id="org1da39c4"></a>

# Introduction


<a id="org36bff9a"></a>

## GUI in C++, lul

I know, right? Whatever happened to using solid frameworks! things like
Electron!  I'm not gonna detail "why not electron" here, not even if it's made
with fearless concurrency; we already know it's shite. Let's move.


<a id="orge2d84f3"></a>

## What is QtQuick

QtQuick is a framework for developing user interfaces with QML. QML is a
declarative markup language made by the Qt Company. It can be used for
several things, like making a [language agnostic build system](https://en.wikipedia.org/wiki/Qbs_(build_tool)).

QtQuick is an altenative to traditional Qt widgets when developing gui. The
interfaces built with it are fluid and ready to be used on any device
without any tweaking. Imagine the beauty of Qt, but without creating visual
components with C++ code. Imagine the beauty of Qt, but without creating
visual components with C++ code!

If you're familiar with Qt widgets (or any other framework really), using
QtQuick will most likely bring you loads of advantages. Things like property
binding, smooth transitions and animations, the whole mobile experience
shenanigans, code reuse, etc.


<a id="orga3206e3"></a>

# First touch


<a id="org920ef66"></a>

## Running qml code


<a id="orge115980"></a>

### qmlscene

To run qml code you only need the `qmlscene` executable included with your
Qt5 install. `qmlscene file.qml` will display the interface described in the
file. This should only be used for debugging and prototyping. If you intend
to deploy or do anything involving real data, you should instead develop a
C++ or a Python application.

1.  Python or C++?

    Right now, the answer is neither. In this guide we will only use qml to
    create a gui without any backend. If you want to go ahead and start using
    Python, note that PySide2 are the latest *officialy supported* Qt bindings
    for Python.


<a id="org374a58c"></a>

### import

Import statements can be used in QML to get access to other qml modules,
javascript, C++ (or Python) types, etc. In this guide the only thing we'll
need to import is the QtQuick module with `import QtQuick 2.9`. You can use
anything between 2.0 and the latest version available to you. Just don't use
1.4 or anything older, unless you have no other choice.


<a id="org5913eef"></a>

### qml file structure

In a qml file you have the import statements at the top and below them a single
top level qml component.
```qml
// file.qml
import QtQuick 2.9

Rectangle {
// everything else goes here
}
```
The `Rectangle` is the most basic *visual* component of QtQuick. It's a
rectangle with usual properties like, x, y, width, height, and also things
like a radius, a color, and so on.


<a id="org0d0de08"></a>

## id and properties

The `id` property is a unique (in the [component scope](https://doc.qt.io/qt-5/qtqml-documents-scope.html#component-scope)) name associated with
each QML component. It's close to the name of a variable, and it's visible
everywhere in the file. This allows you to use the component anywhere within
the file without trouble. In C++ you would declare a variable with `Rectangle
   rect(0, 0, 12, 12);` for a square of height 12 placed at position (0, 0). In
QML you'd write the same as follows:
```qml
Rectangle {
    id: square // no semicolons needed
    x: 0, y: 0 // it's recommended to declare related properties on the same line
    width: 12
    height: width // you can use a property's value to initialize another one

    color: "lightblue"
}
```
Some other properties that are available in a rectangle are `border`,
`gradient`, `opacity`, `visible`, and much [more](https://doc.qt.io/qt-5/qml-qtquick-rectangle-members.html).

Although the `id` looks like one, it's [not a real property](https://doc.qt.io/qt-5/qtqml-syntax-objectattributes.html#the-id-attribute).


<a id="org791864a"></a>

## Nesting

You can also nest elements. This is very useful when you want to create
somewhat complex components, both in look and behaviour:
```qml
Rectangle {
   id: square
   ...
   color: "lightblue"
   Rectangle {
       id: innerBox

       width: 6
       height: width

       // x and y are relative to the parent's coordinates
       // the inner box will ended up centered in its parent
       x: 3, y: 3
   }
}

```
<a id="org6b21b1b"></a>

## Children and parents

When a component is nested inside another one, the child can access its
parent's attributes through the `parent` attribute. The parent can access its
children's through the `children` attribute, which is a list.
```qml
Rectangle {
    id: box
    ...
    radius: innerBox.height / 3 // access any item's properties through its id
    Rectangle {
        id: innerBox
        ...
        // Qt.darker returns the color one shade darker than the one it receives as parameter
        color: Qt.darker(parent.color) // access the parent's properties
    }
}

```
<a id="org3e524f8"></a>

## Reactive programming or property binding

Sometimes you want the user interface you're building to stay consistent
(proportion wise) when the application window is resized or displayed on
screens of different size. For the precedent example, it would be nice to
keep the inner box centered when the parent's proportions change. QtQuick,
QML in general, provides a really neat reactive programming mechanism to
achieve this, property binding. And guess what! We've already been using
it. Indeed, to bind some property to another one it suffices to declare the
former using the later, as we've been doing for the `height` property.
`height: width` When declared like this, everytime the width change, the
height is appropriately updated, so the rectangle is always a square. With
that in mind we can redefine our two rectangles to get even better
reactivity and keep the inner box centered at all times.
```qml
Rectangle {
   // nothing to change
   Rectangle {
       id: innerBox

       width: parent.width
       height: width
       x: (parent.width - width) / 2
       y: (parent.height - height) / 2
       ...
   }
}
```

<a id="org453cbe4"></a>

# Stuff & co.

Rectangles are cool and all, but they are boring. There is so much more to
QML; let's go over some notions. Some of them should look familiar to anyone
who have used Qt before.


<a id="org836548e"></a>

## Adding custom properties

When using QML, one can extend a component by adding new porperties to
it. Say for example we want a certain component to have a name. We could
achieve this with something as simple as: `property string name: "Component
   awesome name"`. This declaration would go inside the component. Note that a
new property doesn't have to be initialized immediately.


<a id="org598628c"></a>

## signals

In the Qt framework, a signal is a predefined message an object sends when a
certain event occurs. They are an indispensable functionality for any
respectable gui framework, under some form or another.
```qml
signal eventOccured // signal declaration

// signal handling
onEventOccured : {
    width = width * 2
}

signal buttonClicked(Position clickPosition) // note that signals can also take parameters

onButtonClicked : {
    // oh no. Is this a javascript
    console.log("x: " + clickPosition.x + " y: " + clickPosition.y)
}
```
A signal is associated with each porperty of every QtQuick component. That
means we could implement handlers for `onWidthChanged`, `onColorChnaged`,
`onRadiusChanged`, etc. This also applies for our own properties. So we
could also implement `onNameChanged`, since we added a name property
previously.


<a id="orgead4612"></a>

## Anchors

An anchor is an attribute that lets you place components relatively to each
other without much struggle. They let you turn a sentence like "above the
status bar, below the menu" into understandable code.
```qml
// tie this component's bottom to the statusbar's top
anchors.bottom: statusBar.top 

// tie this component's top to the menubar's bottom
anchors.top: menuBar.bottom


// make the component fill its parent size
anchors.fill: parent

// centerIn, left and right are other elements that can be used to anchor stuff
```
Note that anchors you can only anchor components to their siblings and
parents.


<a id="org546fa81"></a>

## MouseArea

The mouse area is a basic component that defines an area where mouse events
can be intercepted.  Typically it's declared inside another component that it
fills completely and when the user interact with the said component through
the mouse, those events are available to do awesome stuff.
```qml
Rectangle {
    MouseArea {
        anchors.fill: parent
        onClicked: {
            parent.color: "#e3c003"
        }
    }
}
```

<a id="org32b8cc9"></a>

# Combine all the things


<a id="org54e4c6d"></a>

## Beyonce

At this point, we can already do a lot of cool stuff. Let's make a component
conform to the following specs:

-   Shape: circle
-   Color: toggle between blue and red with mouse click
-   Border color: green
-   Border width: 5 normally, and 0 when the circle is pressed
-   Display the text "Hello, world!" in white, centered in the circle


<a id="org307b60f"></a>

## Additional information

We've already seen most of these. The mouse press event is similar to a click
and it can be handled by implementing `onPressed`. Displaying the text is as
simple as nesting a `Text` component, another basic building block provided
by QtQuick, inside another rectangle. The string it should show can be set
with the `text` attribute, e.g. `text: "What are generics?"`.

I will post a solution to this below, but I would recommend anyone interested
in learning QML to try doing it on their own before checking my
implementation.


<a id="orgcdd9e47"></a>

## Solution
```qml
import QtQuick 2.9

// let's start with a rectangle; almost always start with a rectangle tbh
Rectangle {
    id: button

    signal clicked // we will trigger this signal when the button is clicked

    // when the signal is triggered, we'll toggle the color
    onClicked: {
        // Qt.colorEqual is used to compare colors
        // btw you can specify colors in many formats
        // e.g: "blue", "#0000ff", "#ff0000ff" and many more
        // including hsv and hsl
        // here we use strings
        color =  Qt.colorEqual(color, "blue") ? "red" : "blue"
    }

    width: 50
    height: width
    radius: width / 2 // make the rectangle a circle

    color: "blue"
    border.color: "green"

    border.width: {
        // pressed is a read-only boolean property of MouseArea
        mouseArea.pressed ? 0 : 5
    }

    Text {
        id: label

        anchors.centerIn: parent
        color: "white"
        text: "Hello, world!"
    }

    MouseArea {
        id: mouseArea
        anchors.fill: parent

        // note that clicked() is a function call
        // the parentheses are necessary
        onClicked: button.clicked()
    }
}
```
Now that you're initiated to QtQuick, the electron fanboys better watch out.
