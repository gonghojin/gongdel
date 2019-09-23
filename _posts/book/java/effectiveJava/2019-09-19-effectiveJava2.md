---
layout: post
comments: true
title:  "이펙티브 자바 3/E_모든 객체의 공통 메서드"
date:   2019-09-19 22:00:00
author: Gongdel
categories: Book
tags:	 Java Book EffectiveJava
cover:  "/assets/instacode.png"
---
# 3장. 모든 객체의 공통 메서드
## 10. equals는 일반 규약을 지켜 재정의하라!
equals 메서드는 재정의하기 쉬워 보이지만 곳곳에 함정이 도사리고 있어서, 올바른 재정의가 필요하다.  
다음에서 열거한 상황 중 하나에 해당한다면 재정의하지 않는 것이 최선이다.
+ 각 인스턴스가 본질적으로 고유하다.
	+ 값을 표현하는 게 아니라 동작하는 개체를 표현하는 클래스가 여기 해당한다.  
	Thread가 좋은 예로, object의 equals 메서드는 이러한 클래스에 딱 맞게 구현되었다.
+ 인스턴스의 '논리적 동치성(logical eqaulity)'을 검사할 일이 없다.
+ 상위 클래스에서 재정의한 equals가 하위 클래스에도 딱 들어맞는다.
+ 클래스가 private이거나 package-private이고 equals 메서드를 호출할 일이 없다.

그렇다면 equals를 재정의해야 할 때는 언제일까?  
객체 식별성(두 객체가 물리적으로 같은가)이 아니라 논리적 동치성을 확인해야 하는데, 상위 클래스의 equals가 논리적 동치성을 비교하도록 재정의되지 않았을 때다.  
주로 값 클래스들(Integer와 String처럼 값을 표현하는 클래스)이 여기 해당한다. (두값 객체를 eqauls로 비교 시 객체가 같은지가 아니라 값이 같은지를 알고 싶어하기 때문)    

##### equals 메서드를 재정희 할 떄는 반드시 일반 규약을 따라야 하며, 다음은 Object 명세에 적힌 규약이다.
equals 메서드는 동치 관계를 구현하며, 다음을 만족한다.
+ 반사성: null이 아닌 모든 참조 값 x에 대해 x.equals(x)는 true다
+ 대칭성: null이 아닌 모든 참조 값 x, y에 대해, x.equals(y)가 true면 y.equals(x)도 true다. 
+ 추이성: null이 아닌 모든 참조 값 x, y, z에 대해, x.equals(y)가 true이고 y.equals(z)도 true면 x.equals(z)도 true다
+ 일관성
+ null-아님: null이 아닌 모든 참조 값 x에 대해, x.equals(null)은 false다.

그렇다면 Object 명세에서 말하는 동치관계란 무엇일까? 쉽게 말해, 집합을 서로 같은 원소들로 이뤄진 부분집합으로 나누는 연산이다.  
이 부분집을 동치 클래스라 한다. equals 메서드가 쓸모 있으려면 모든 원소가 같은 동치 클래스에 속한 어떤 원소와도 서로 교환할 수 있어야 한다.  

이제 동치관계를 만족시키기 위한 다섯 요건을 하나씩 살펴보자.

#### 반사성
단순히 말하면 객체는 자기 자신과 같아야 한다는 뜻으로 일부러 어기는 경우가 아니라면 만족시키지 못하기가 더 어려움

#### 대칭성
두 객체는 서로에 대한 동치 여부에 똑같이 답해야 한다는 뜻이다.  

#### 추이성
첫 번째 객체와 두 번째 객체가 같고, 두 번쨰 객체와 세 번쨰 객체가 같다면, 첫 번째 객체와 세 번째 객체도 같아야 한다는 뜻이다.  
