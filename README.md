# Apple_Document_Translation
文档原文地址：https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html

Nib Files Nib文件

Nib files play an important role in the creation of applications in OS X and iOS. With nib files, you create and manipulate your user interfaces graphically, using Xcode, instead of programmatically. Because you can see the results of your changes instantly, you can experiment with different layouts and configurations very quickly. You can also change many aspects of your user interface later without rewriting any code.

For applications built using the AppKit or UIKit frameworks, nib files take on an extra significance. Both of these frameworks support the use of nib files both for laying out windows, views, and controls and for integrating those items with the application’s event handling code. Xcode works in conjunction with these frameworks to help you connect the controls of your user interface to the objects in your project that respond to those controls. This integration significantly reduces the amount of setup that is required after a nib file is loaded and also makes it easy to change the relationships between your code and user interface later.

Note: Although you can create an Objective-C application without using nib files, doing so is very rare and not recommended. Depending on your application, avoiding nib files might require you to replace large amounts of framework behavior to achieve the same results you would get using a nib file.

Anatomy of a Nib File Nib文件分解

A nib file describes the visual elements of your application’s user interface, including windows, views, controls, and many others. It can also describe non-visual elements, such as the objects in your application that manage your windows and views. Most importantly, a nib file describes these objects exactly as they were configured in Xcode. At runtime, these descriptions are used to recreate the objects and their configuration inside your application. When you load a nib file at runtime, you get an exact replica of the objects that were in your Xcode document. The nib-loading code instantiates the objects, configures them, and reestablishes any inter-object connections that you created in your nib file.

nib文件描述了可视化的应用界面元素，包括windows、controls、等。它也可以描述非可视化的元素，比如管理windows和views的元素。更重要的是，nib文件还可以精确地描述那些在Xcode中展示的那样的objects。在运行的时候，这些描述被用来重新创建objects及其配置（像继承、依赖、关联等）。当你在运行时加载一个nib文件的时候，你可以得到想你在Xcode中编辑的那样的副本。加载nib文件的代码，将会实例化、配置那些描述的objects；并且会按照你创建的nib文件中的那样，重新建立这些objects之间的关系。

The following sections describe how nib files used with the AppKit and UIKit frameworks are organized, the types of objects found in them, and how you use those objects effectively.

下面的这些sections描述了nib文件是如何被AppKit&UIKit frameworks




