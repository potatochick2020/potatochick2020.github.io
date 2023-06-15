---
layout: post
title: "C++ Qt Core vs Qt Quick vs Qt QML vs Qt Widget "
tags: ["C++","GUI","Qt QML","Qt Quick","Qt Core", "Qt Widget"]
categories: ["C++","GUI","Qt"]
---

## Qt Core

> The Qt Core module provides core non-GUI functionality to C++. It adds features such as a powerful mechanism for seamless object communication called signals and slots, queryable and designable object properties, hierarchical and queryable object trees that organize object ownership in a natural way with guarded pointers (QPointer), and a dynamic cast that works across library boundaries1.
> Qt Core also provides thread support in the form of platform-independent threading classes, a thread-safe way of posting events, and signal-slot connections across threads. It also provides a resource system for organizing application files and assets, a set of containers, and classes for receiving input and printing output.

Qt core is basically a main part of Qt which provide similar functionality like Standard Template Library.

## Qt Quick and Qt QML

> Qt Quick is a library for creating user interfaces using QML, a declarative language for designing UI-centric applications. It provides a way to build fluid, animated and touch-enabled user interfaces. Qt Quick includes a visual canvas and an associated scripting language called QML.

Qt Quick and Qt QML Provide the UI part, and it is cross architecture , e.g. could be use in smart fridge, television, or anyware. Where Qt QUICk is the library, and QML is more a description of the UI.

## Qt Widget

> Qt Widgets is the traditional desktop-oriented UI model. It supports menus, toolbars, dialogs, and other standard desktop behaviors extremely well2. You can mix QML with a Qt Widgets application using the QQuickWidget class3.

Qt widget is an older and an project stopped developing anymore, but there are still a lot of company using it.

[Qt widget: not deprecated, but no longer developed](https://news.ycombinator.com/item?id=19297095)