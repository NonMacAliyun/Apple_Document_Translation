文档原文地址：https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html

##### Nib Files （Nib文件）

Nib files play an important role in the creation of applications in OS X and iOS. With nib files, you create and manipulate your user interfaces graphically, using Xcode, instead of programmatically. Because you can see the results of your changes instantly, you can experiment with different layouts and configurations very quickly. You can also change many aspects of your user interface later without rewriting any code.

For applications built using the AppKit or UIKit frameworks, nib files take on an extra significance. Both of these frameworks support the use of nib files both for laying out windows, views, and controls and for integrating those items with the application’s event handling code. Xcode works in conjunction with these frameworks to help you connect the controls of your user interface to the objects in your project that respond to those controls. This integration significantly reduces the amount of setup that is required after a nib file is loaded and also makes it easy to change the relationships between your code and user interface later.

Note: Although you can create an Objective-C application without using nib files, doing so is very rare and not recommended. Depending on your application, avoiding nib files might require you to replace large amounts of framework behavior to achieve the same results you would get using a nib file.

##### Anatomy of a Nib File （Nib文件分解）

A nib file describes the visual elements of your application’s user interface, including windows, views, controls, and many others. It can also describe non-visual elements, such as the objects in your application that manage your windows and views. Most importantly, a nib file describes these objects exactly as they were configured in Xcode. At runtime, these descriptions are used to recreate the objects and their configuration inside your application. When you load a nib file at runtime, you get an exact replica of the objects that were in your Xcode document. The nib-loading code instantiates the objects, configures them, and reestablishes any inter-object connections that you created in your nib file.

nib文件描述了可视化的应用界面元素，包括windows、controls、等。它也可以描述非可视化的元素，比如管理windows和views的元素。更重要的是，nib文件还可以精确地描述那些在Xcode中展示的那样的objects。在运行的时候，这些描述被用来重新创建objects及其配置（像继承、依赖、关联等）。当你在运行时加载一个nib文件的时候，你可以得到想你在Xcode中编辑的那样的副本。加载nib文件的代码，将会实例化、配置那些描述的objects；并且会按照你创建的nib文件中的那样，重新建立这些objects之间的关系。

The following sections describe how nib files used with the AppKit and UIKit frameworks are organized, the types of objects found in them, and how you use those objects effectively.

下面的这些sections描述了nib文件是如何被AppKit&UIKit frameworks组织，如何被发现类型，如何有效的利用。

##### About Your Interface Objects （关于interface的对象）

Interface objects are what you add to an nib file to implement your user interface. When a nib is loaded at runtime, the interface objects are the objects actually instantiated by the nib-loading code. Most new nib files have at least one interface object by default, typically a window or menu resource, and you add more interface objects to a nib file as part of your interface design. This is the most common type of object in a nib file and is typically why you create nib files in the first place.

Interface objects 是那些在nib文件中用来实现应用界面的东西。当nib文件被运行时加载的时候，这些 interface objects 通过 **nib加载代码**被实例化。大多数的nib文件含有至少一个 interface object，具有代表性的像：window、menu或者那些你添加了很多 interface objects 的界面。

Besides representing visual objects, such as windows, views, controls, and menus, interface objects can also represent non-visual objects. In nearly all cases, the non-visual objects you add to a nib file are extra controller objects that your application uses to manage the visual objects. Although you could create these objects in your application, it is often more convenient to add them to a nib file and configure them there. Xcode provides a generic object that you use specifically when adding controllers and other non-visual objects to a nib file. It also provides the controller objects that are typically used to manage Cocoa bindings.

除了表示虚拟的对象（windows、view、controls、menus），interface objects还能表示非虚拟的对象。在几乎所有的情况中，向nib文件中添加的非虚拟的对象是 应用中用来管理那些虚拟对象的 控制器外的附加对象。Xcode提供了一个你可以明确使用的通用对象，以便向nib中添加控制器或者非虚拟对象；同时还提供了控制器对象用来管理Cocoa绑定。

##### About the File’s Owner （关于File‘s Owner）

One of the most important objects in a nib file is the File’s Owner object. Unlike interface objects, the File’s Owner object is a placeholder object that is not created when the nib file is loaded. Instead, you create this object in your code and pass it to the nib-loading code. The reason this object is so important is that it is the main link between your application code and the contents of the nib file. More specifically, it is the controller object that is responsible for the contents of the nib file.

在nib文件中最重要的对象之一是File's owner。不像其他的interface objects，File’s Owner是一个占位对象，在nib文件被创建的时候它并不会被创建。而是在代码中创建并将其做参数传递给加载nib的方法。File’s Owner如此重要是因为它可以将代码和nib文件中的对象关联起来。具体说来就是，控制器中的对象是要对nib文件中的内容负责的。

In Xcode, you can create connections between the File’s Owner and the other interface objects in your nib file. When you load the nib file, the nib-loading code recreates these connections using the replacement object you specify. This allows your object to reference objects in the nib file and receive messages from the interface objects automatically.

在Xcode中，可以创建File’s Owner和nib文件中interface objects的关联。当程序运行时加载nib文件的时候，加载代码重新创建这些对象们的关联，这样就可以让你的objects引用nib文件中的objects并自动接收其消息。

##### About the First Responder（关于第一响应者）

In a nib file, the First Responder is a placeholder object that represents the first object in your application’s dynamically determined responder chain. Because the responder chain of an application cannot be determined at design time, the First Responder placeholder acts as a stand-in target for any action messages that need to be directed at the application’s responder chain. ~~Menu items commonly target the First Responder placeholder. For example, the Minimize menu item in the Window menu hides the frontmost window in an application, not just a specific window, and the Copy menu item should copy the current selection, not just the selection of a single control or view.~~ Other objects in your application can target the First Responder as well.

![FirstResponder图片](https://raw.githubusercontent.com/NonMacAliyun/Apple_Document_Translation/master/NibFile_FirstResponder.png)

在nib文件中，First Responder是一个占位对象，代表应用中动态确定的响应者链中的链首的那个对象。因为程序编译的时候响应者链不能确定，First Responder占位对象表现的像一个替身目标。

When you load a nib file into memory, there is nothing you have to do to manage or replace the First Responder placeholder object. The AppKit and UIKit frameworks automatically set and maintain the first responder based on the application’s current configuration.

当加载nib文件到内存的时候，不需要做任何事来管理、替换第一响应者。AppKit（OS X）、UIKit会自动自动设置、持有基于应用的当前配置的第一响应者。

For more information about the responder chain and how it is used to dispatch events in AppKit–based applications, see Event Architecture inCocoa Event Handling Guide. For information about the responder chains and handling actions in iPhone applications, see Event Handling Guide for iOS.

想了解更过关于响应者链及其如何在AppKit中分配事件，请移步Event Architecture inCocoa Event Handling Guide。想了解iOS应用中响应者链以及事件操控，请移步 Event Handling Guide for iOS。

##### About the Top-Level Objects（关于Top-Level对象）

When your program loads a nib file, Cocoa recreates the entire graph of objects you created in Xcode. This object graph includes all of the windows, views, controls, cells, menus, and custom objects found in the nib file. The top-level objects are the subset of these objects that do not have a parent object. The top-level objects typically include only the windows, menu bars, and custom controller objects that you add to the nib file. (Objects such as File’s Owner, First Responder, and Application are placeholder objects and not considered top-level objects.)

当程序加载nib文件的时候，Cocoa重新创建全部在Xcode中创建的对象表。对象表包括所有的window、view、control、cell、menu、自定义对象。top-level对象是没有父类的对象们的子集。

Typically, you use outlets in the File’s Owner object to store references to the top-level objects of a nib file. If you do not use outlets, however, you can retrieve the top-level objects from the nib-loading routines directly. You should always keep a pointer to these objects somewhere because your application is responsible for releasing them when it is done using them. For more information about the nib object behavior at load time, see Managing the Lifetimes of Objects from Nib Files.

通常的，使用outlets来保存对nib文件中top-level对象的引用。如果不使用outlets，则可以在nib加载的时候直接检索。需要始终维持一个指向nib文件对象的指针，因为应用负责在不使用它们的时候释放它们。想了解更多有关nib对象在load time 的过程，请移步Managing the Lifetimes of Objects from Nib Files。