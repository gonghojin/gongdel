---
layout: post
comments: true
title:  "이펙티브 자바 3/E_클래스와 인터페이스"
date:   2019-09-28 22:00:00
author: Gongdel
categories: Book
tags:	 Java Book EffectiveJava
cover:  "/assets/instacode.png"
---
# 4장. 클래스와 인터페이스
## 15. 클래스와 멤버의 접근 권한을 최소화하라
### 핵심 정리
프로그램 요소의 접근성은 `가능한 한 최소한으로 하라.` 꼭 필요한 것만 골라 최소한의 public API를 설계하자.  
그 외에는 클래스, 인터페이스, 멤버가 의도치 않게 API로 공개되는 일이 없도록 해야 한다.  
+ public 클래스는 상수용 public static final 필드 외에는 어떠한 public 필드도 가져서는 안 된다.  
+ public static final 필드가 참조하는 객체가 불변인지 확인하라.

## 16. public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라
### 핵심 정리
public 클래스는 `절대 가변 필드를 직접 노출해서는 안 된다.` 불변 필드라면 노출해도 덜 위험하지만 완전히 안심할 수는 없다.  
하지만 package-private 클래스나 private 중첩 클래스에서는 종종 (불변이든 가변이든) 필드를 노출하는 편이 나을 때도 있다.

## 17. 변경 가능성을 최소화하라
불변 클래스를 만들려면 5 가지 규칙을 따르면 된다.
+ 객체의 상태를 변경하는 메서드(변경자)를 제공하지 않는다.
+ 클래스를 확장할 수 없도록 한다.
	+ 하위 클래스에서 객체의 상태를 변하게 만드는 사태를 막아준다.
	+ final 클래스
	+ private 필드, private 생성자, 정적 팩토리 사용
+ 모든 필드를 final로 선언한다.
+ 모든 필드를 private로 선언한다.
+ 자신 외에는 내부의 가변 컴포넌트에 접근할 수 없도록 한다.