# DesignBehavior : 行为型模式
## 1. 策略模式
### 数据结构
>IStrategy： 策略接口
>ConcreteStrategy：具体策略实现
>StrategyContext：策略上下文，会持有一个具体策略对象，对外提供客户端可以调用的方法
### 测试类
```java
 public static void main(String[] args) {
        System.out.println("我知道策略1，请给我一个idea");
        //首先进行策略1
        ConcreteStrategy1 concreteStrategy1 = new ConcreteStrategy1();
        StrategyContext context = new StrategyContext(concreteStrategy1);
        System.out.println(context.giveAnIdea());

        System.out.println("我改主意了，想用策略2，请重新给我一个idea");
        ConcreteStrategy2 concreteStrategy2 = new ConcreteStrategy2();
        context = new StrategyContext(concreteStrategy2);
        System.out.println(context.giveAnIdea());

    }
```
## 2. 
？
## 3. 
？
## 4. 
？
## 5. 
？
## 6. 
？
## 7. 
？
## 8. 
？
## 8. 
？
## 10. 
？
## 11. 
？