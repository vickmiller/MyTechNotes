#[Advanced Memory Management Programming Guide](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html)

##About Memory Management

> Although memory management is typically considered at the level of an individual object, your goal is actually to manage object graphs. You want to make sure that you have no more objects in memory than you actually need.

![mm](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/MemoryMgmt/Art/memory_management_2x.png)

##At a Glance

> Objective-C provides two methods of application memory management.
>
> - In the method described in this guide, referred to as “manual retain-release” or MRR, you explicitly manage memory by keeping track of objects you own. This is implemented using a model, known as reference counting, that the Foundation class NSObject provides in conjunction with the runtime environment.


> - In Automatic Reference Counting, or ARC, the system uses the same reference counting system as MRR, but it inserts the appropriate memory management method calls for you at compile-time. You are strongly encouraged to use ARC for new projects. If you use ARC, there is typically no need to understand the underlying implementation described in this document, although it may in some situations be helpful. For more about ARC, see Transitioning to ARC Release Notes.

大体上来说，OC提供两种方式让程序管理内存：

- MRR "manual retain-release" 手动保留-释放
- ARC "Automatic Reference Counting" 自动引用计数




##[Memory Management Policy](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmRules.html#//apple_ref/doc/uid/20000994-BAJHFBGH) 内存管理策略

##[Practical Memory Management](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW1) 实践

##[Using Autorelease Pool Blocks](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmAutoreleasePools.html#//apple_ref/doc/uid/20000047-CJBFBEDI) 使用自动释放池块

相关引用

| [NSAutoreleasePool](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Classes/NSAutoreleasePool_Class/index.html#//apple_ref/occ/cl/NSAutoreleasePool) | 自动释放池              |
| :--------------------------------------- | :----------------- |
| [NSCopying](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSCopying_Protocol/index.html#//apple_ref/occ/intf/NSCopying) | 拷贝                 |
| [NSMutableCopying](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSMutableCopying_Protocol/index.html#//apple_ref/occ/intf/NSMutableCopying) | 对象的可变拷贝（拷贝对象并令其可变） |
| [NSObject_Class](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Classes/NSObject_Class/index.html#//apple_ref/occ/cl/NSObject) |                    |
| [NSObject_Protocol](https://developer.apple.com/library/prerelease/ios/documentation/Cocoa/Reference/Foundation/Protocols/NSObject_Protocol/index.html#//apple_ref/occ/intf/NSObject) |                    |