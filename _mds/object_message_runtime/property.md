#属性

> An Objective-C property is a public or private method declared with the @property syntax.

Objective-C里的属性就是使用@property语法做公开或私有的方法声明。



> Properties capture the state of an object. They reflect the object’s intrinsic attributes and relationships to other objects. Properties provide a safe, convenient way to interact with these attributes without having to write a set of custom accessor methods (although properties do allow custom getters and setters, if desired).

用了属性，首先你可以省去写内部变量的getters和setters。属性反应对象的本质特性以及与其他对象的关系。如果有需要的话，你甚至可以自定义setters和getters。

##Benefits

> Using properties instead of instance variables in as many places as possible provides many benefits:
>
> - Autosynthesized getters and setters. When you declare a property, by default getter and setter methods are created for you.
> 

> - Better declaration of intent of a set of methods. Because of accessor method naming conventions, it’s clear exactly what the getter and setter are doing.
> 

> - Property keywords that express additional information about behavior. Properties provide the potential for declaration of attributes like assign (vs copy), weak, atomic (vs nonatomic), and so on.

尽可能的使用属性代替实例变量，你会获得如下这些便利：

- **自动合成getters和setters。**你声明了属性，编译器默认会给你创建好setters和getters
- xxx
- **属性的一些关键字代表了很多额外的行为控制信息。**如assign、weak、atomic等诸多关键字。

##Naming Convention

> Property methods follow a simple naming convention. The getter is the name of the property (for example, date), and the setter is the name of the property with the set prefix, written in camel case (for example, setDate). The naming convention for Boolean properties is to declare them with a named getter starting with the word “is”:
>
> `@property (readonly, getter=isBlue) BOOL blue;`
>
> As a result, all of the following work:
>
> `if (color.blue) { }`
> `if (color.isBlue) { }`
> `if ([color isBlue]) { }`

属性对应的方法命名采用的是驼峰命名法，getter就是属性名称，setter加上set前缀。Boolean类型的属性的getter通常使用is前缀。

形如上边三种表达方式是一样的效果。



##Never Do This!!

> When deciding what can be a property, keep in mind that the following are not properties:
>
> - init method
> - copy method, mutableCopy method
> - A class factory method
> - A method that initiates an action and returns a BOOL result
> - A method that explicitly changes internal state as a side effect of a getter

别在init方法里使用





