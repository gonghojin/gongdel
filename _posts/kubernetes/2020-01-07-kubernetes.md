---
layout: post
comments: true
title:  "쿠버네티스(Kubernetes) 기본 주요 개념"
date:   2020-01-06 00:00:00
author: Gongdel
categories: Kubernetes
tags:	 Kubernetes
cover:  "/assets/instacode.png"
---

# 쿠버네티스의 주요 개념

리소스 |용도 |
------------ | -------------| 
노드         | 컨테이너가 배치되는 서버
네임스페이스   | 쿠버네티스 클러스터 안의 가상 클러스터
파드             | 컨테이너의 집합 중 가장 작은 단위로, 컨테이너의 실행 방법을 정의
레플리카세트(replica Sets)| 같은 스펙을 갖는 파드를 여러 개 생성하고 관리하는 역할 
디플로이먼트(Deploymets) | 레플리카 세트의 리비전을 관리
서비스            | 파드의 집합에 접근하기 위한 경로를 정의
인그레스(Ingress)    | 서비스를 쿠버네티스 클러스터 외부로 노출시킨다.
컨피그맵(Config Mpas)       | 설정 정보를 정의하고 파드에 전달
퍼시스턴트 볼륨(Persistent Volume) | 파드가 사용할 스토리지의 크기 및 종류를 정의
퍼시스턴트 볼륨 클레임(Persistent Volume Claim) | 퍼시스턴트 볼륨을 동적으로 확보
스토리지 클래스(Storage class)            | 퍼시스턴트 볼륨을 확보하는 스토리지의 종류를 정의 
스테이트풀 세트(Stateful Sets)     | 같은 스펙으로 모두 동일한 파드를 여러 개 생성하고 관리
잡(Job)					| 상주 실행을 목적으로 하지 않는 파드를 여러 개 생성하고 정상적인 종료를 보장
크론잡(Clon Jobs)		| 크론 문법으로 스케줄링되는 잡.

---

# 쿠버네티스 클러스터와 노드
+ 쿠버네티스 클러스터
	- 쿠버네티스의 여러 리소스를 관리하기 위한 집합체
		- 쿠버네티스 리소스 중에서 가장 큰 개념은 노드(Node)
	- 적어도 하나 이상의 마스터(서버)에 의해 관리를 받음
+ 노드
	- 쿠버네티스 클러스터의 관리 대상으로 등록된 도커 호스트
	- 컨테이너가 배치되는 대상