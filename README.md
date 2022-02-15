# NoteBook
学习笔记

# 1. 如何发现代码质量问题？
* 目录设置是否合理、模块划分是否清晰、代码结构是否满足“高内聚、松耦合”？
* 是否遵循经典的设计原则和设计思想（SOLID、DRY、KISS、YAGNI、LOD 等）？
* 设计模式是否应用得当？是否有过度设计？
* 代码是否容易扩展？如果要添加新功能，是否容易实现？
* 代码是否可以复用？是否可以复用已有的项目代码或类库？是否有重复造轮子？
* 代码是否容易测试？单元测试是否全面覆盖了各种正常和异常的情况？
* 代码是否易读？是否符合编码规范（比如命名和注释是否恰当、代码风格是否一致等）？

> 以上是一些通用的关注点，可以作为常规检查项，套用在任何代码的重构上。除此之外，我们还要关注代码实现是否满足业务本身特有的功能和非功能需求。我罗列了一些比较有共性的问题，如下所示。这份列表可能还不够全面，剩下的需要你针对具体的业务、具体的代码去具体分析。  

* 代码是否实现了预期的业务需求？
* 逻辑是否正确？是否处理了各种异常情况？
* 日志打印是否得当？是否方便 debug 排查问题？
* 接口是否易用？是否支持幂等、事务等？
* 代码是否存在并发问题？是否线程安全？
* 性能是否有优化空间，比如，SQL、算法是否可以优化？
* 是否有安全漏洞？比如输入输出校验是否全面？  

# 2. 最常用的评价标准有哪几个？
最常用到几个评判代码质量的标准有：可维护性、可读性、可扩展性、灵活性、简洁性、可复用性、可测试性。其中，可维护性、可读性、可扩展性又是提到最多的、最重要的三个评价标准。  

# 3. 设计原则  
SOLID 原则：SRP 单一职责原则  
--------------------------------
一个类只负责完成一个职责或者功能。单一职责原则通过避免设计大而全的类，避免将不相关的功能耦合在一起，来提高类的内聚性。同时，类职责单一，类依赖的和被依赖的其他类也会变少，减少了代码的耦合性，以此来实现代码的高内聚、松耦合。但是，如果拆分得过细，实际上会适得其反，反倒会降低内聚性，也会影响代码的可维护性。不同的应用场景、不同阶段的需求背景、不同的业务层面，对同一个类的职责是否单一，可能会有不同的判定结果。实际上，一些侧面的判断指标更具有指导意义和可执行性，比如，出现下面这些情况就有可能说明这类的设计不满足单一职责原则：  
   * 类中的代码行数、函数或者属性过多；
   * 类依赖的其他类过多或者依赖类的其他类过多；
   * 私有方法过多；
   * 比较难给类起一个合适的名字；
   * 类中大量的方法都是集中操作类中的某几个属性。  
  
  
SOLID 原则：OCP 开闭原则
--------------------------------
对扩展开放、修改关闭  
  

SOLID 原则：LSP 里式替换原则
--------------------------------
子类对象（object of subtype/derived class）能够替换程序（program）中父类对象（object of base/parent class）出现的任何地方，并且保证原来程序的逻辑行为（behavior）不变及正确性不被破坏。  

SOLID 原则：ISP 接口隔离原则
--------------------------------
接口隔离原则的描述是：客户端不应该强迫依赖它不需要的接口。其中的“客户端”，可以理解为接口的调用者或者使用者。理解“接口隔离原则”的重点是理解其中的“接口”二字。这里有三种不同的理解。  
如果把“接口”理解为一组接口集合，可以是某个微服务的接口，也可以是某个类库的接口等。如果部分接口只被部分调用者使用，我们就需要将这部分接口隔离出来，单独给这部分调用者使用，而不强迫其他调用者也依赖这部分不会被用到的接口。  
如果把“接口”理解为单个 API 接口或函数，部分调用者只需要函数中的部分功能，那我们就需要把函数拆分成粒度更细的多个函数，让调用者只依赖它需要的那个细粒度函数。  
如果把“接口”理解为 OOP 中的接口，也可以理解为面向对象编程语言中的接口语法。那接口的设计要尽量单一，不要让接口的实现类和调用者，依赖不需要的接口函数。  
单一职责原则针对的是模块、类、接口的设计。接口隔离原则相对于单一职责原则，一方面更侧重于接口的设计，另一方面它的思考的角度也是不同的。接口隔离原则提供了一种判断接口的职责是否单一的标准：通过调用者如何使用接口来间接地判定。如果调用者只使用部分接口或接口的部分功能，那接口的设计就不够职责单一。    


SOLID 原则：DIP 依赖倒置原则  
--------------------------------
* 控制反转：实际上，控制反转是一个比较笼统的设计思想，并不是一种具体的实现方法，一般用来指导框架层面的设计。这里所说的“控制”指的是对程序执行流程的控制，而“反转”指的是在没有使用框架之前，程序员自己控制整个程序的执行。在使用框架之后，整个程序的执行流程通过框架来控制。流程的控制权从程序员“反转”给了框架。
* 依赖注入：依赖注入和控制反转恰恰相反，它是一种具体的编码技巧。我们不通过 new 的方式在类内部创建依赖类的对象，而是将依赖的类对象在外部创建好之后，通过构造函数、函数参数等方式传递（或“注入”）给类来使用。
* 依赖注入框架：我们通过依赖注入框架提供的扩展点，简单配置一下所有需要的类及其类与类之间的依赖关系，就可以实现由框架来自动创建对象、管理对象的生命周期、依赖注入等原本需要程序员来做的事情。
* 依赖反转原则：依赖反转原则也叫作依赖倒置原则。这条原则跟控制反转有点类似，主要用来指导框架层面的设计。高层模块不依赖低层模块，它们共同依赖同一个抽象。抽象不需要依赖具体实现细节，具体实现细节依赖抽象。  



