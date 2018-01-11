---
layout: post

title: 设计模式之单例模式
tags: 设计模模式 
---

## 单例模式

#### <span style="color:red">概念</span>：单个实例，也就是一个类有且仅有一个实例，并且自行实例化向整个系统提供。

#### 单例模式又分为两种：

	
	饿汉模式：

	public class Singleton {

    private Singleton(){}

    private static Singleton singleton = new Singleton();

    public static Singleton getInstance(){
        return singleton;
    }
	}	

	懒汉模式
	public class Singleton2 {
    
    private Singleton2(){}

    private static Singleton2 singleton2;

    public static Singleton2 getInstance(){
        if(singleton2==null){
            singleton2 = new Singleton2();
        }
        return singleton2;
    }
	}	


## 饿汉模式与懒汉模式的区别

#### 1、饿汉模式加载类的时候创建实例，获取对象的速度比较快。懒汉反之

#### 2、在线程安全的问题上，饿汉模式是线程安全的，懒汉模式是不安全的。在并发访问的时候，很多线程同时访问了getInstance()方法，并发现singleton2为空，则都会执行 singleton2 = new Singleton2()这样就创建了多个singleton2实例，不符合单例模式的设计思想，所以懒汉模式是不安全的。