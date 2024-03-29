![alt text](image-2.png)


C++前向声明

C++的类可以进行前向声明。但是，仅仅进行前向声明而没有定义的类是不完整的，这样的类，只能用于定义指针、引用、以及用于函数形参的指针和引用。

```cpp
class Widget; // Widget is a forward declaration

void doSomething(Widget* pW);
void doSomething(Widget&);