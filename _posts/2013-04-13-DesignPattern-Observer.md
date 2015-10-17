---
layout: post
title: 无脑理解JAVA观察者模式
date: 2014-04-13
categories: blog
tags: [java,DesignPattern,Observer,观察者]
description: 无脑理解JAVA观察者模式结。


---
###无脑理解JAVA观察者模式
不扯概念了,用一个简单的事例来说明:

比如办公室里每天有人在悄悄聊QQ,老板从外面回来的时候有个人会通知办公室的人赶紧把QQ关掉,这个人即为通知者,而那些办公室的人则为订阅者.

详情看代码

    package com.hebo.test;
    //通知者接口
    //用接口的原因是,可能通知同事的人不是前台,前台如果请假了,可能是清洁工大妈,也有可能是老板自己,或者是其他人
    interface Subject{
        void Attach(Observer observer);//添加要通知的同事,比如某个同事你不想通知就不用添加
        void Detach(Observer observer);//删除要通知的同事,比如某个同事请假今天不在
        void Notify();	//通知方法,自定义 比如老板来了~~ 老板娘来了~~...
        String getAction();
    }
    
然后今天是一个清洁工人来通知大家:

    package com.hebo.test;
    import java.util.ArrayList;
    import java.util.List;
    /**
    * 我是清洁工人,我看见老板来了就会告诉你们~
    * 也可以声明其他类来实现这个接口,比如前台类,老板类...
    * @author HeBo
    */
    public class Dustman implements Subject {

    	//同事列表
    	private List<Observer> observers = new ArrayList<Observer>();
    	private String action;
    	
    	//增加一个同事(小伙子我看好你,以后我帮你盯着点老板)
    	@Override
    	public void Attach(Observer observer) {
    		observers.add(observer);
    	}
    
    	//减少一个同事(某某请假就不需要通知了)
    	@Override
    	public void Detach(Observer observer) {
    		observers.remove(observer);
    	}
    
    	//通知同事集合里的小伙子们
    	@Override
    	public void Notify() {
    		for (Observer o : observers) {
    			o.Update();
    		}
    	}
    
    	public String getAction() {
    		return action;
    	}
    
    	public void setAction(String action) {
    		this.action = action;
    	}
    }
    
要被通知的同事类:

    package com.hebo.test;
    /**
    * 同事类
    * @author HeBo
    * 为什么用抽象类?Update方法完全可以写死,但是可能有些同事在聊QQ,有的同事偷偷打游戏,就会有不同的方法体
    */
    public abstract class Observer {
    	 String name;
    	 Subject sub;//通知者,谁来通知我老板来了
    	
    	public Observer(String name, Subject sub) {
    		super();
    		this.name = name;
    		this.sub = sub;
    	}
    	
    	public abstract void Update();
    }
    
有个聊QQ的同事:

    package com.hebo.test;
    /**
    * 我是一个在偷偷聊QQ的同学~
    * @author HeBo
    * 也可以用其他类继承Observer,比如在偷偷打游戏的,偷偷看片的~
    */
    public class QQColleague extends Observer {

    	public QQColleague(String name, Subject sub) {
    		super(name, sub);
    	}
    
    	@Override
    	public void Update() {
    		System.out.println(sub.getAction()+"来了,"+name+"赶紧关闭QQ继续工作~");
    	}
    }
    
测试:

    package com.hebo.test;
    public class Test {

    	public static void main(String[] args) {
    		//清洁工人
    		Dustman d = new Dustman();
    		//聊QQ的同事
    		QQColleague qc = new QQColleague("张三", d);
    		
    		//加入通知的集合里
    		d.Attach(qc);
    		
    		d.setAction("老板李四我回来了~");
    
    		d.Notify();
    	}
    }
    
运行结果:
老板李四我回来了~来了,张三赶紧关闭QQ继续工作~
