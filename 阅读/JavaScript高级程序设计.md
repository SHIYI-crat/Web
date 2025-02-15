# JavaScript高级程序设计

# 1、什么是JavaScript

* JavaScript是一门用来与网页交互的脚本语言，包含以下三个组成部分。
  * ECMAScript:由ECMA-262定义并提供核心功能。
  * 文档对象模型(DOM):提供与**网页内容**交互的方法和接口。
  * 浏览器对象模型（BOM):提供与**浏览器**交互的方法和接口。
* JavaScript的这三个部分得到了五大Web浏览器(正、Firefox、Chrome、Safari和Opera)不同程度的支持。所有浏览器基本上对ES5(ECMAScript 5)提供了完善的支持，而对ES6(ECMAScript 6)和ES7 (ECMAScript7)的支持度也在不断提升。这些浏览器对DOM的支持各不相同，但对Leve13的支持日益趋于规范。HTML5中收录的BOM 会因浏览器而异，不过开发者仍然可以假定存在很大一部分公共特性。



# 2、HTML中的JavaScript

* 要包含外部JavaScript文件，必须将src属性设置为要包含文件的URL。文件可以跟网页在同一台服务器上，也可以位于完全不同的域。
* 所有< script>元素会依照它们在网页中出现的次序被解释。在不使用defer和async属性的情况下，包含在< script>元素中的代码必须严格按次序解释。
* 对不推迟执行的脚本，浏览器必须解释完位于< script>元素中的代码，然后才能继续渲染页面的剩余部分。为此，通常应该把< script>元素放到页面末尾，介于主内容之后及< /body>标签之前。
* 可以**使用defer 属性把脚本推迟到文档渲染完毕后再执行**。推迟的脚本原则上按照它们被列出的次序执行。
* 可以**使用async属性表示脚本不需要等待其他脚本**，同时也不阻塞文档渲染，即异步加载。异步脚本不能保证按照它们在页面中出现的次序执行。
* 通过**使用< noscript>元索，可以指定在浏览器不支持脚本时显示的内容**。如果浏览器支持并启用脚本，则< noscript>元素中的任何内容都不会被渲染。



# 3、语言基础

* 严格模式

~~~JavaScript
function doSomething(){
    "use strict";
    //函数体
}
~~~

* **var/let/const：**

~~~js
//1、var函数作用域 函数的局部变量
function test1(){
    var message = "hi";//局部变量
}
test1();
console.log(message);//出错

//省略var 全局变量 不推荐
function test2(){
    message = "hi";
}
test2();
console.log(message)//"hi"

//2、var变量提升 把所有变量声明都拉到函数作用域的顶部

//let块作用域
if(true){
    let age = 26;
    console.log(age);//26
}
console.log(age)//age没有定义

//1、暂时性死区 let声明的变量不会在作用域中被提升
//2、var声明的变量会成为window对象的属性，let不会
//3、条件声明 不检查是否已声明
//4、let之前，for循环定义的迭代变量会渗透到循环体外部

//const 的行为与let基本相同，唯一一个重要的区别是用它声明变量时必须同时初始化变量，且尝试修改const声明的变量会导致运行时错误
~~~

* Number( )函数基于如下规则执行转换:布尔值，true转换为1， false转换为0;数值，直接返回;null，返回0;undefined，返回NaN;字符串，应用规则。

* ECMAScript中的基本数据类型包括Undefined、Null、Boolean 、Number(不区分整数和浮点值) 、String 和Symbol;Object是一种复杂数据类型，它是这门语言中所有对象的基类。
* ECMAScript提供了C语言和类C语言中常见的很多基本操作符,包括数学操作符、布尔操作符、关系操作符、相等操作符和赋值操作符等。
* ECMAScript中的函数与其他语言中的函数不一样。不指定返回值的函数实际上会返回特殊值undefined。



# 4、变量、作用域与内存

* JavaScript变量可以保存两种类型的值:原始值和引用值。原始值可能是以下6种原始数据类型之一:Undefined、Null、Boolean、Number、String和symbol。原始值和引用值有以下特点。
* 原始值大小固定，因此保存在栈内存上。从一个变量到另一个变量复制原始值会创建该值的第二个副本。
* 引用值是对象，存储在堆内存上。包含引用值的变量实际上只包含指向相应对象的一个指针，而不是对象本身。从一个变量到另一个变量复制引用值只会复制指针，因此结果是两个变量都指向同一个对象。
* typeof操作符可以确定值的原始类型，而instanceof操作符用于确保值的引用类型。
* 任何变量（不管包含的是原始值还是引用值)都存在于某个执行上下文中(也称为作用域)。这个上下文（作用域）决定了变量的生命周期，以及它们可以访问代码的哪些部分。执行上下文分全局上下文、函数上下文和块级上下文。
* 代码执行流每进入一个新**上下文**，都会创建一个作用域链，用于搜索变量和函数。函数或块的局部上下文不仅可以访问自己作用域内的变量，而且也可以访问任何包含上下文乃至全局上下文中的变量。全局上下文只能访问全局上下文中的变量和函数，不能直接访问局部上下文中的任何数据。变量的执行上下文用于确定什么时候释放内存。
* JavaScript是使用**垃圾回收**的编程语言，离开作用域的值会被自动标记为可回收，然后在垃圾回收期间被删除。主流的垃圾回收算法是标记清理，即先给当前不使用的值加上标记，再回来回收它们的内存。
* **引用计数**是另一种垃圾回收策略，需要记录值被引用了多少次。JavaScript引擎不再使用这种算法，但某些旧版本的正仍然会受这种算法的影响，原因是JavaScript会访问非原生JavaScript对象（如DOM元素)。引用计数在代码中存在循环引用时会出现问题。
* **解除变量的引用**不仅可以消除循环引用，而且对垃圾回收也有帮助。为促进内存回收，全局对象、全局对象的属性和循环引用都应该在不需要时解除引用。



# 5、基本引用类型

* 引用值与传统面向对象编程语言中的类相似，但实现不同。ECMAScript **缺少传统的面向对象编程语言所具备的某些基本结构，包括类和接口**。引用类型有时候也被称为对象定义，因为它们描述了自己的对象应有的属性和方法。
* Date类型提供关于日期和时间的信息，包括当前日期、时间及相关计算。
* RegExp类型是ECMAScript支持正则表达式的接口，提供了大多数基础的和部分高级的正则表达式功能。存在**模式局限**(分别匹配字符串的开始和末尾、条件式匹配、正则表达式注释)。
* JavaScript 比较独特的一点是，**函数实际上是Function类型的实例，也就是说函数也是对象**。因为函数也是对象，所以函数也有方法，可以用于增强其能力。
* 由于原始值包装类型的存在，JavaScript 中的原始值可以被当成对象来使用。有3种原始值包装类型:Boolean、Nurmber和 string。它们都具备如下特点。
  * 每种包装类型都映射到同名的原始类型。
  * 以读模式访问原始值时，后台会实例化一个原始值包装类型的对象，借助这个对象可以操作相应的数据。
  * 涉及原始值的语句执行完毕后，包装对象就会被销毁。
* 当代码开始执行时，全局上下文中会存在两个内置对象:Global和 Math。其中，Global对象在大多数ECMAScript实现中无法直接访问。不过，浏览器将其实现为window对象。所有全局变量和函数都是Global对象的属性。Math对象包含辅助完成复杂计算的属性和方法。



# 6、集合引用类型

* JavaScript中的对象是引用值，可以通过几种内置引用类型创建特定类型的对象。引用类型与传统面向对象编程语言中的类相似，但实现不同。
* Object类型是一个基础类型，所有引用类型都从它继承了基本的行为。
* Array类型表示一组有序的值，并提供了操作和转换值的能力。
* 定型数组包含一套不同的引用类型，用于管理数值在内存中的类型。
* ECMAScript6新增了一批引用类型:Map、weakMap、Set和 weakSet。这些类型为组织应用程序数据和简化内存管理提供了新能力。



# 7、迭代器与生成器

* ECMAScript 6正式支持迭代模式并引入了两个新的语言特性:迭代器和生成器。迭代会在一个**有序集合**上进行。(“有序”可以理解为集合中所有项都可以按照既定的顺序被遍历到，特别是开始和结束项有明确的定义。）数组是JavaScript中有序集合的最典型例子。
* 迭代器是一个可以由任意对象实现的接口，支持连续获取对象产出的每一个值。任何实现itarable接口的对象都有一个Symbol.iterator属性，这个属性引用默认迭代器。默认迭代器就像一个迭代器工厂，也就是一个函数，调用之后会产生一个实现iterator接口的对象。
* 迭代器必须通过连续调用**naxt()**方法才能连续取得值，这个方法返回一个**Iteratorobject**。这个对象包含一个done 属性和一个value 属性。前者是一个布尔值，表示是否还有更多值可以访问;后者包含迭代器返回的当前值。这个接口可以通过手动反复调用next ()方法来消费，也可以通过原生消费者，比如for-of循环来自动消费。
* 生成器是一种特殊的函数，调用之后会返回一个生成器对象。生成器对象实现了Iterable接口，因此可用在任何消费可迭代对象的地方。生成器的独特之处在于支持 yield关键字，这个关键字能够暂停执行生成器函数。使用yield关键字还可以通过next()方法接收输人和产生输出。在加上星号之后，yield关键字可以将跟在它后面的可迭代对象序列化为一连串值。



# 8、对象、类与面向对象编程

* 属性的类型:
  * 数据属性
    * `Configurable`：是否可以通过delete删除并重新定义，是否可以修改它的特性，是否可以把它改为访问器属性
    * `Enumerable`：是否可以通过for-in循环返回
    * `Writable`：表示属性的值是否可以被修改
    * `Value`：包含属性实际的值
  * 访问器属性
    * `Configurable`：是否可以通过delete删除并重新定义，是否可以修改它的特性，是否可以把它改为访问器属性
    * `Enumerable`：是否可以通过for-in循环返回
    * `Get`：获取函数，读取属性时调用
    * `Set`：设置函数，写入属性时调用
* 对象解构赋值 ：嵌套解构、部分解构、参数上下文匹配
* 对象在代码执行过程中的任何时候都可以被创建和增强(mixin)，具有极大的动态性，并不是严格定义的实体。下面的模式适用于创建对象。
  * **工厂模式**就是一个简单的函数**(creatxxx)**，这个函数可以创建对象，为它添加属性和方法，然后返回这个对象。这个模式在构造函数模式出现后就很少用了。
  * 使用**构造函数模式**可以自定义引用类型，可以使用**new关键字**像创建内置类型实例一样创建自定义类型的实例。不过，构造函数模式也有不足，主要是其成员无法重用，包括函数。考虑到函数本身是松散的、弱类型的，没有理由让函数不能在多个对象实例间共享。
  * **原型模式**解决了成员共享的问题，只要是添加到构造函数**prototype** 上的属性和方法就可以共享。而组合构造函数和原型模式通过构造函数定义实例属性，通过原型定义共享的属性和方法。
* 对象迭代：Object.values()(返回对象值)和Object.entries()(返回键/值)接受一个对象，返回它们内容的数组。
* JavaScript 的**继承**主要通过**原型链**来实现。**原型链涉及把构造函数的原型赋值为另一个类型的实例**。这样一来，子类就可以访问父类的所有属性和方法，就像基于类的继承那样。原型链的问题是所有继承的属性和方法都会在对象实例间共享，无法做到实例私有。
* **盗用构造函数模式**通过在子类构造函数中调用父类构造函数，可以避免这个问题。这样可以让每个实例继承的属性都是私有的，但要求类型只能通过构造函数模式来定义(因为子类不能访问父类原型上的方法)。
* 目前最流行的继承模式是**组合继承**，即通过原型链继承共享的属性和方法，通过盗用构造函数继承实例属性。
* 除上述模式之外，还有以下几种继承模式。
  * 原型式继承可以无须明确定义构造函数而实现继承，本质上是对给定对象执行浅复制。这种操作的结果之后还可以再进一步增强。
  * 与原型式继承紧密相关的是**寄生式继承**，即先基于一个对象创建一个新对象，然后再增强这个新对象，最后返回新对象。这个模式也被用在组合继承中，用于避免重复调用父类构造函数导致的浪费。
  * **寄生组合继承**被认为是实现基于类型继承的最有效方式。
* ECMAScript 6新增的类很大程度上是基于既有原型机制的语法糖。类的语法让开发者可以优雅地定义向后兼容的类，既可以继承内置类型，也可以继承自定义类型。类有效地跨越了对象实例、对象原型和对象类之间的鸿沟。



# 9、代理与反射

* 代理是ECMAScript 6新增的令人兴奋和动态十足的新特性。尽管不支持向后兼容，但它开辟出了一片前所未有的JavaScript元编程及抽象的新天地。
* 从宏观上看，代理是真实JavaScript对象的透明抽象层。代理可以定义包含捕获器的处理程序对象，而这些捕获器可以拦截绝大部分JavaScript 的基本操作和方法。在这个捕获器处理程序中，可以修改任何基本操作的行为，当然前提是遵从**捕获器不变式**。(target,handler)
* 与代理如影随形的反射API，则封装了一整套与捕获器拦截的操作相对应的方法。可以把**反射**API看作一套基本操作，这些操作是绝大部分JavaScript对象API的基础。(Refelct)
* 代理的应用场景是不可限量的。开发者使用它可以创建出各种编码模式，比如(但远远不限于)跟踪属性访问、隐藏属性、阻止修改或删除属性、函数参数验证、构造函数参数验证、数据绑定，以及可观察对象。



# 10、函数

* 函数表达式与函数声明是不一样的。函数声明要求写出函数名称，而函数表达式并不需要。没有名称的函数表达式也被称为匿名函数。
* ES6新增了类似于函数表达式的箭头函数语法，但两者也有一些重要区别。(箭头函数不能使用arguments，super和new.target，也不能做构造函数。箭头函数也没有prototype属性)
* JavaScript中函数定义与调用时的参数极其灵活。arguments对象,以及ES6新增的扩展操作符，可以实现函数定义和调用的完全动态化。
* 函数内部也暴露了很多对象和引用，涵盖了函数被谁调用、使用什么调用，以及调用时传入了什么参数等信息。
* JavaScript引擎可以优化符合尾调用条件的函数，以节省栈空间。
* 闭包的作用域链中包含自己的一个变量对象，然后是包含函数的变量对象，直到全局上下文的变量对象。
* 通常，函数作用域及其中的所有变量在函数执行完毕后都会被销毁。
* 闭包在被函数返回之后，其作用域会一直保存在内存中，直到闭包被销毁。
* 函数可以在创建之后立即调用，执行其中代码之后却不留下对函数的引用。
* 立即调用的函数表达式如果不在包含作用域中将返回值赋给一个变量，则其包含的所有变量都会被销毁。
* 虽然JavaScript没有私有对象属性的概念，但可以使用闭包实现公共方法，访问位于包含作用域中定义的变量。
* 可以访问私有变量的公共方法叫作特权方法。
* 特权方法可以使用构造函数或原型模式通过自定义类型中实现，也可以使用模块模式或模块增强模式在单例对象上实现。



# 11、期约与异步函数

* 长期以来，掌握单线程JavaScript运行时的异步行为一直都是个艰巨的任务。随着ES6新增了期约和ES8新增了异步函数，ECMAScript 的异步编程特性有了长足的进步。通过期约和 async/await，不仅可以实现之前难以实现或不可能实现的任务，而且也能写出更清晰、简洁,并且容易理解、调试的代码。
* 期约的主要功能是为异步代码提供了清晰的抽象。可以用期约表示异步执行的代码块，也可以用期约表示异步计算的值。在需要串行异步代码时，期约的价值最为突出。作为可塑性极强的一种结构，期约可以被序列化、连锁使用、复合、扩展和重组。
* 异步函数是将期约应用于JavaScript 函数的结果。异步函数可以暂停执行，而不阻塞主线程。无论是编写基于期约的代码，还是组织串行或平行执行的异步代码，使用异步函数都非常得心应手。异步函数可以说是现代JavaScript工具箱中最重要的工具之一。



# 12、BOM

* 浏览器对象模型(BOM，Browser Object Model)是以window对象为基础的，这个对象代表了浏览器窗口和页面可见的区域。**window对象也被复用为ECMAScript的global对象**，因此所有全局变量和函数都是它的属性，而且所有原生类型的构造函数和普通函数也都从一开始就存在于这个对象之上。
* 要引用其他window对象，可以使用几个不同的窗口指针。
* 通过location对象可以以编程方式操纵浏览器的导航系统。通过设置这个对象上的属性可以改变浏览器URL中的某一部分或全部。
* 使用replace()方法可以替换浏览器历史记录中当前显示的页面，并导航到新URL。
* navigator对象提供关于浏览器的信息。提供的信息类型取决于浏览器，不过有些属性如userAgent是所有浏览器都支持的。
* BOM中的另外两个对象也提供了一些功能。screen对象中保存着客户端显示器的信息。这些信息通常用于评估浏览网站的设备信息。history对象提供了操纵浏览器历史记录的能力，开发者可以确定历史记录中包含多少个条目，并以编程方式实现在历史记录中导航，而且也可以修改历史记录。



# 13、客户端检测

* 客户端检测是JavaScript 中争议最多的话题之一。因为不同浏览器之间存在差异，所以经常需要根据浏览器的能力来编写不同的代码。客户端检测有不少方式，但下面两种用得最多。
* **能力检测**，在使用之前先测试浏览器的特定能力。例如，脚本可以在调用某个函数之前先检查它是否存在。这种客户端检测方式可以让开发者不必考虑特定的浏览器或版本，而只需关注某些能力是否存在。能力检测不能精确地反映特定的浏览器或版本。
* **用户代理检测**，通过用户代理字符串确定浏览器。用户代理字符串包含关于浏览器的很多信息，通常包括浏览器、平台、操作系统和浏览器版本。用户代理字符串有一个相当长的发展史，很多浏览器都试图欺骗网站相信自己是别的浏览器。用户代理检测也比较麻烦，特别是涉及Opera会在代理字符串中隐藏自己信息的时候。即使如此，用户代理字符串也可以用来确定浏览器使用的渲染引擎以及平台，包括移动设备和游戏机。
* 在选择客户端检测方法时，首选是使用能力检测。特殊能力检测要放在次要位置，作为决定代码逻辑的参考。用户代理检测是最后一个选择，因为它过于依赖用户代理字符串。
* 浏览器也提供了一些软件和硬件相关的信息。这些信息通过screen和 navigator对象暴露出来。利用这些API，可以获取关于操作系统、浏览器、硬件、设备位置、电池状态等方面的准确信息。



# 14、DOM

* 文档对象模型(DOM，Document Object Model)是语言中立的HTML和XML文档的API。DOMLevell将HTML和XML文档定义为一个节点的多层级结构，并暴露出JavaScript 接口以操作文档的底层结构和外观。
* DOM由一系列节点类型构成，主要包括以下几种。
* Node是基准节点类型，是文档一个部分的抽象表示，所有其他类型都继承Node。
* Document类型表示整个文档，对应树形结构的根节点。在JavaScript中,document对象是Document 的实例，拥有查询和获取节点的很多方法。
* Element节点表示文档中所有HTML或XML元素，可以用来操作它们的内容和属性。
* 其他节点类型分别表示文本内容、注释、文档类型、CDATA区块和文档片段。
* DOM编程在多数情况下没什么问题,在涉及< script >和< style >元素时会有一点兼容性问题
  因为这些元素分别包含脚本和样式信息，所以浏览器会将它们与其他元素区别对待。
* 要理解 DOM，最关键的一点是知道影响其性能的问题所在。DOM操作在JavaScript代码中是代价比较高的，NodeList对象尤其需要注意。NodeList对象是“实时更新”的，这意味着每次访问它都会执行一次新的查询。考虑到这些问题，实践中要尽量减少DOM操作的数量。
* Mutation0bserver是为代替性能不好的MutationEvent而问世的。使用它可以有效精准地监控DOM变化,而且API也相对简单。



# 15、DOM扩展

* 虽然DOM规定了与XML和HTML文档交互的核心API，但其他几个规范也定义了对 DOM的扩展。很多扩展都基于之前的已成为事实标准的专有特性标准化而来。本章主要介绍了以下3个规范。
* Selectors API为基于CSS选择符获取DOM元素定义了几个方法:**queryselector ( )、queryselectorAll ( )和l matches ( )。**
* **Element Traversa**l在DOM元素上定义了额外的属性,以方便对DOM元素进行遍历。这个需求是因浏览器处理元素间空格的差异而产生的。
* HTML5为标准DOM提供了大量扩展。其中包括对innerHTML 属性等事实标准进行了标准化，还有焦点管理、字符集、滚动等特性。
* DOM扩展的数量总体还不大，但随着Web技术的发展一定会越来越多。浏览器仍然没有停止对专有扩展的探索，如果出现成功的扩展，那么就可能成为事实标准，或者最终被整合到未来的标准中。



# 16、DOM2和DOM3

* DOM2规范定义了一些模块，用来丰富DOM1的功能。DOM2 Core在一些类型上增加了与XML命名空间有关的新方法。这些变化只有在使用XML或XHTML文档时才会用到，在HTML文档中则没有用处。DOM2增加的与XML命名空间无关的方法涉及以编程方式创建Document和 DocumentType类型的新实例。
* DOM2 Style模块定义了如何操作元素的样式信息。
  * 每个元素都有一个关联的style对象，可用于确定和修改元素特定的样式。
  * 要确定元素的计算样式,包括应用到元素身上的所有CSS规则,可以使用**getComputedstyle** ( )方法。
  * 通过document.stylesheets 集合可以访问文档上所有的样式表。
* DOM2 Traversal and Range模块定义了与DOM结构交互的不同方式。
  * **NodeIterator和Treewalker**可以对DOM树执行深度优先的遍历。
  * NodeIterator接口很简单，每次只能向前和向后移动一步。Treewalker 除了支持同样的行为，还支持在DOM结构的所有方向移动，包括父节点、同胞节点和子节点。
  * 范围是选择DOM结构中特定部分并进行操作的一种方式。
  * 通过范围的选区可以在保持文档结构完好的同时从文档中移除内容，也可复制文档中相应的部分。



# 17、事件

* 事件是JavaScript与网页结合的主要方式。最常见的事件是在DOM3 Events规范或HTML5中定义的。虽然基本的事件都有规范定义，但很多浏览器在规范之外实现了自己专有的事件，以方便开发者更好地满足用户交互需求，其中一些专有事件直接与特殊的设备相关。
* DOM事件流，包括**事件冒泡和事件捕获**
* 事件类型：
  * 用户界面事件（UIEvent ):涉及与BOM交互的通用浏览器事件
  * 焦点事件( FocusEvent ):在元素获得和失去焦点时触发
  * 鼠标事件（MouseEvent ):使用鼠标在页面上执行某些操作时触发
  * 滚轮事件( wheelEvent ):使用鼠标滚轮（或类似设备）时触发
  * 输入事件(工nputEvent ):向文档中输人文本时触发
  * 键盘事件(KeyboardEvent ):使用键盘在页面上执行某些操作时触发
  * 合成事件( CompositionEvent ):在使用某种IME ( Input Method Editor，输人法编辑器）输人字符时触发
* 围绕着使用事件，需要考虑内存与性能问题。例如:
  * 最好限制一个页面中事件处理程序的数量，因为它们会占用过多内存，导致页面响应缓慢;
  * 利用事件冒泡，**事件委托**可以解决限制事件处理程序数量的问题;
  * 最好在页面卸载之前删除所有事件处理程序。
* 使用JavaScript 也可以在浏览器中模拟事件。DOM2 Events和 DOM3 Events规范提供了模拟方法，可以模拟所有原生 DOM事件。键盘事件一定程度上也是可以模拟的，有时候需要组合其他技术。IE8及更早版本也支持事件模拟，只是接口与DOM方式不同。
* 事件是JavaScript中最重要的主题之一，理解事件的原理及其对性能的影响非常重要。



# 18、动画与Canvas图形

* **requestAnimationFrame**是简单但实用的工具，可以让JavaScript 跟进浏览器渲染周期，从而更加有效地实现网页视觉动效。
* HTML5的<canvas>元素为JavaScript 提供了动态创建图形的API。这些图形需要使用特定上下文绘制，主要有两种。第一种是支持基本绘图操作的**2D上下文**:
  * 填充和描绘颜色及图案
  * 绘制矩形
  * 绘制路径
  * 绘制文本
  * 创建渐变和图案

* 第二种是**3D上下文，也就是WebGL**。WebGL是浏览器对OpenGL ES 2.0的实现。OpenGL ES 2.0是游戏图形开发常用的一个标准。WebGL支持比2D上下文更强大的绘图能力，包括:
  * 用OpenGL着色器语言（ GLSL)编写顶点和片段着色器;
  * 支持定型数组，限定数组中包含数值的类型;
  * 创建和操作纹理。
* 目前所有主流浏览器的较新版本都已经支持<canvas>标签。



# 19、表单脚本

* 尽管HTML和Web应用自诞生以来已经发生了天翻地覆的变化，但Web表单几乎从来没有变过。JavaScript可以增加现有的表单字段以提供新功能或增强易用性。为此，表单字段也暴露了属性方法和事件供 JavaScript使用。以下是一些概念：
  * 可以使用标准或非标准的方法全部或部分选择文本框中的文本。
  * 所有浏览器都采用了Firefox操作文本选区的方式，使其成为真正的标准。
  * 可以通过监听键盘事件并检测要插人的字符来控制文本框接受或不接受某些字符。
* 所有浏览器都支持剪贴板相关的事件，包括copy、cut和 paste。剪贴板事件在不同浏览器中的实现有很大差异。
* 在文本框只限某些字符时，可以利用剪贴板事件屏幕粘贴事件。
* 选择框也是经常使用JavaScript来控制的一种表单控件。借助DOM,操作选择框比以前方便了很多。使用标准的DOM技术，可以为选择框添加或移除选项，也可以将选项从一个选择框移动到另一个选择框，或者重排选项。
* 富文本编辑通常以使用包含空白HTML文档的内嵌窗格来处理。通过将文档的designMode属性设置为" on "，可以让整个页面变成编辑区，就像文字处理软件一样。另外，给元素添加 contenteditable属性也可以将元素转换为可编辑区。默认情况下，可以切换文本的粗体、斜体样式，也可以使用剪贴板功能。JavaScript通过execCommand()方法可以执行一些富文本编辑功能,通过queryCommandEnabled () 、queryCommandstate()和 queryCommandValue ()方法则可以获取有关文本选区的信息。由于富文本编辑区不涉及表单字段,因此要将富文本内容提交到服务器,必须把HTML从iframe或contenteditable元素中复制到一个表单字段。



# 20、JavaScript API

* 除了定义新标签，HTML5还定义了一些JavaSctipt API。这些API可以为开发者提供更便捷的Web接口，暴露堪比桌面应用的能力。本章主要介绍了以下 API。
* Atomics API用于保护代码在多线程内存访问模式下不发生资源争用，同一时刻只能对缓冲区执行一个操作。
* postMessage ( ) API支持从不同源**跨文档发送消息**，同时保证安全和遵循同源策略。
* Encoding API 用于实现字符串与缓冲区之间的无缝转换（越来越常见的操作)。
* File API提供了发送、接收和读取大型二进制对象的可靠工具。
* 媒体元素<audio>和<video>拥有自己的API，用于操作音频和视频。并不是每个浏览器都会支持所有媒体格式，使用canPlayType ( )方法可以检测浏览器支持情况。
* 拖放API支持方便地将元素标识为可拖动，并在操作系统完成放置时给出回应。可以利用它创建自定义可拖动元素和放置目标。
* Notifications API提供了一种浏览器中立的方式，以此向用户展示消通知弹层。
* Streams API支持以全新的方式读取、写入和处理数据。
* Timing API提供了一组度量数据进出浏览器时间的可靠工具。
* Web Components API为元素重用和封装技术向前迈进提供了有力支撑。
* Web Cryptography API让生成随机数、加密和签名消息成为一类特性。



# 21、错误处理与调试

* 对于今天复杂的Web应用程序而言，JavaScript 中的错误处理十分重要。未能预测什么时候会发生错误以及如何从错误中恢复，会导致糟糕的用户体验，甚至造成用户流失。大多数浏览器默认不向用户报告JavaScript错误，因此在开发和调试时需要自己实现错误报告。不过在生产环境中，不应该以这种方式报告错误。
* 下列方法可用于阻止浏览器对JavaScript错误作出反应。
  * 使用**try/catch**语句，可以通过更合适的方式对错误做出处理，避免浏览器处理。(finally)
  * 定义**window.onerror**事件处理程序,所有没有通过try/catch处理的错误都会被该事件处理程序接收到（仅限IE、Firefox和 Chrome )。
* 开发Web应用程序时，应该认真考虑可能发生的错误，以及如何处理这些错误。
  * 首先，应该分清哪些算重大错误，哪些不算重大错误。
  * 然后，要通过分析代码预测很可能发生哪些错误。由于以下因素，JavaScript中经常出现错误:
    * 类型转换;(**类型转换错误**)
    * 数据类型检测不足;(**数据类型错误**)
    * 向服务器发送错误数据或从服务器接收到错误数据。(通信错误)
* IE、Firefox、Chrome、Opera和 Safari都有JavaScript调试器，有的内置在浏览器中，有的是作为扩展，需另行下载。所有调试器都能够设置断点、控制代码执行和在运行时检查变量值。



# 22、处理XML

* 浏览器对使用JavaScript处理XML实现及相关技术相当支持。然而，由于早期缺少规范，常用的功能出现了不同实现。DOM Level2提供了创建空XML文档的API，但不能解析和序列化。浏览器为解析和序列化XML实现了两个新类型。
  * **DOMParser类型**是简单的对象，可以将XML字符串解析为DOM文档。
  * **XMLSerializer类型**执行相反操作，将DOM文档序列化为XML字符串。
* 基于所有主流浏览器的实现，DOMLevel3新增了针对XPathAPI的规范。该API可以让 JavaScript针对DOM文档执行任何XPath查询并得到不同数据类型的结果。
* 最后一个与XML相关的技术是XSLT,目前并没有规范定义其API。Firefox最早增加XSLTProcessor类型用于通过JavaScript处理转换。



# 23、JSON

* JSON是一种轻量级数据格式,可以方便地表示简单/复杂数据结构。这个格式使用JavaScript 语法的一个子集表示对象、数组、字符串、数值、布尔值和null。虽然XML也能胜任同样的角色，但JSON更简洁，JavaScript支持也更好。更重要的是，所有浏览器都已经原生支持全局JSON对象。
* ECMAScript 5定义了原生JSON对象，用于将JavaScript对象序列化为JSON字符串,以及将JSON数组解析为JavaScript对象。**JSON.stringify()**和**JSON.parse()**方法分别用于实现这两种操作。这两个方法都有一些选项可以用来改变默认的行为，以实现过滤或修改流程。



# 24、网络请求与远程资源

* Ajax是无须刷新当前页面即可从服务器获取数据的一个方法，具有如下特点。
  * 让Ajax迅速流行的中心对象是**XMLHttpRequest** (XHR )。
  * 这个对象最早由微软发明,并在E5中作为通过JavaScript 从服务器获取XML数据的一种手段。
  * 之后，Firefox、Safari、Chrome和 Opera都复刻了相同的实现。W3C随后将XHR行为写入 Web
    标准。
  * 虽然不同浏览器的实现有些差异，但XHR对象的基本使用在所有浏览器中相对是规范的，因此
    可以放心地在Web应用程序中使用。
  * XMLHttpRequest，实际上是过时Web规范的产物，应该只在旧版本浏览器中使用。实际开发中，应该尽可能使用**fetch ( )**。
* XHR的一个主要限制是同源策略，即通信只能在相同域名、相同端口和相同协议的前提下完成。访问超出这些限制之外的资源会导致安全错误，除非使用了正式的跨域方案。这个方案叫作**跨源资源共享**(CORS，Cros-Origin Resource Sharing )，XHR对象原生支持CORS。图片探测和JSONP是另外两种跨域通信技术，但没有CORS可靠。
* **Fetch API**是作为对XHR对象的一种端到端的替代方案而提出的。这个API提供了优秀的基于期约的结构、更直观的接口，以及对Stream API的最好支持。
* **Web Socket**是与服务器的全双工、双向通信渠道。与其他方案不同, Web Socket不使用HTTP而使用了自定义协议，目的是更快地发送小数据块。这需要专用的服务器，但速度优势明显。



# 25、客户端存储

* **Web Storage**定义了两个对象用于存储数据: sessionStorage和 localStorage。前者用于严格保存浏览器一次会话期间的数据,因为数据会在浏览器关闭时被删除。后者用于会话之外持久保存数据。
* **IndexedDB**是类似于SQL数据库的结构化数据存储机制。不同的是，IndexedDB存储的是对象而不是数据表。对象存储是通过定义键然后添加数据来创建的。游标用于查询对象存储中的特定数据，而索引可以针对特定属性实现更快的查询。
* 有了这些存储手段,就可以在客户端通过使用JavaScript存储可观的数据。因为这些数据没有加密,所以要注意不能使用它们存储敏感信息。

 



# 26、模块

* **模块模式**是管理复杂性的永恒工具。开发者可以通过它创建逻辑彼此独立的代码段，在这些代码段之间声明依赖，并将它们连接在一起。此外，这种模式也是经证明能够优雅扩展到任意复杂度且跨平台的方案。
* 多年以来，CommonJS和AMD这两个分别针对服务器端环境和受延迟限制的客户端环境的模块系统长期分裂。两个系统都获得了爆炸性增强，但为它们编写的代码则在很多方面不一致，经常也会带有冗余的样板代码。而且，这两个系统都没有在浏览器中实现。缺乏兼容导致出现了相关工具，从而让在浏览器中实现模块模式成为可能。
* ECMAScript 6规范重新定义了浏览器模块,集之前两个系统之长于一身,并通过更简单的声明性语法暴露出来。浏览器对原生模块的支持越来越好，但也提供了稳健的工具以实现从不支持到支持ES6模块的过渡。



# 27、工作者线程

* 工作者线程可以运行异步JavaScript而不阻塞用户界面。这非常适合复杂计算和数据处理，特别是需要花较长时间因而会影响用户使用网页的处理任务。工作者线程有自己独立的环境，只能通过异步消息与外界通信。
* 工作者线程可以是**专用线程、共享线程**。专用线程只能由一个页面使用，而共享线程则可以由同源的任意页面共享。
* **服务工作者线程**用于让网页模拟原生应用程序。服务工作者线程也是一种工作者线程，但它们更像是网络代理，而非独立的浏览器线程。可以把它们看成是高度定制化的网络缓存，它们也可以在 PWA中支持推送通知。



# 28、最佳实践

* 随着JavaScript开发日益成熟，最佳实践不断涌现。曾经的业余爱好如今也成为了正式的职业。因此，前端开发也需要像其他编程语言一样，注重可维护性、性能优化和部署。
* 为保证JavaScript代码的**可维护性（容易理解、符合常识、容易适配、容易扩展、容易调试）**，可以参考如下编码惯例。
  * 其他语言的编码惯例可以作为添加注释和确定缩进的参考，但JavaScript作为一门适合松散类型的语言也有自己的一些特殊要求。
  * 由于JavaScript必须与HTML和CSS共存，因此**各司其职**尤为重要:JavaScript负责定义行为，HTML负责定义内容，而CSS负责定义外观。
  * 如果三者职责混淆，则可能导致难以调试的错误和可维护性问题。
  * 随着Web应用程序中JavaScript代码量的激增，**性能**也越来越重要。因此应该牢记如下这些事项。
  * 执行JavaScript所需的时间直接影响网页性能，其重要性不容忽视。
  * 很多适合C语言的性能优化策略同样也适合JavaScript，包括循环展开和使用switch语句而不是if语句。
  * 另一个需要重视的方面是 DOM交互很费时间，因此应该尽可能限制DOM操作的数量。开发Web应用程序的最后一步是上线部署。
  * 为辅助部署，应该建立构建流程，将JavaScript文件合并为较少的(最好是只有一个)文件。
  * 构建流程可以实现很多源代码处理任务的自动化。例如，可以运行JavaScript验证程序，确保没有语法错误和潜在的问题。
  * 压缩可以让文件在部署之前变得尽量小。
  * 启用HTTP压缩可以让网络传输的JavaScript文件尽可能小，从而提升页面的整体性能。

