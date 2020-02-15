# Abstract Factory

## Intent

提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。

## Code

``` C++
Class AbstractProductA {}
Class AbstractProductB {}
Class ProductA1 : AbstractProductA {}
Class ProductA2 : AbstractProductA {}
Class ProductB1 : AbstractProductB {}
Class ProductB2 : AbstractProductB {}

Class AbstractFactory
{
  virtual AbstractProductA CreateProductA() = 0;
  virtual AbstractProductB CreateProductB() = 0; 
}

Class ConcreteFactory1 : AbstractFactory
{
  virtual AbstractProductA CreateProductA() { return new ProductA1; }
  virtual AbstractProductB CreateProductB() { return new ProductB1; } 
}

Class ConcreteFactory2 : AbstractFactory
{
  virtual AbstractProductA CreateProductA() { return new ProductA2; }
  virtual AbstractProductB CreateProductB() { return new ProductB2; } 
}
```