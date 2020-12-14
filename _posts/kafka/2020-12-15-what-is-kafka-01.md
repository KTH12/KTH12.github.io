---
title: "도대체 카프카란?(1)"
layout: archive
date: 2020-12-15
---

-------------------------------------------------

## 카프카를 알게 된 계기

서비스를 분산화 하고, 여러 도메인 서비스에서 발생하는 이벤트를 받아  
분산처리를 할 수 있는 아키텍처를 찾고 있었습니다.  
그럴러면, 마이크로 서비스들이 서로 서로 이벤트를 받아야 하는데,  
이러한 아키텍처를 구현 할 수 있는 쉽고 강력한 도구가 없을까? 라는 생각을 하게 되었습니다.    
그러던중, 카프카라는 강력한 플랫폼을 알게 되었고  
알면알수록 매력적으로 다가왔습니다. 

## 위키백과가 말해주는 카프카란?

>아파치 카프카는 아파치 소프트웨어 재단이 스칼라로 개발한 오픈 소스 메시지 브로커 프로젝트이다. 이 프로젝트는 실시간 데이터 피드를 관리하기 위해 통일된, 높은 처리량, 낮은 지연시간을 지닌 플랫폼을 제공하는 것이 목표이다.  
>개발된곳은 링크드인이고, 2011년초 최종적으로 오픈소스화 되었다.   
>> 카프카를 사용하는 기업  
>> 애플,카카오 (기업),이베이,넷플릭스,페이팔,Uber,월마트  
>> (알만한 기업들은 모두 사용!)

## Confluent가 말하는 카프카란? (Confluent는 링크드인 카프카 개발자가 만든 회사)

>Apache Kafka는 하루에 수조 개의 이벤트를 처리 할 수있는 커뮤니티 분산 이벤트 스트리밍 플랫폼입니다. 처음에는 메시징 큐로 인식 된 Kafka는 분산 커밋 로그의 추상화를 기반으로합니다. 2011 년 LinkedIn에서 만들고 오픈 소스로 만든 이후 Kafka는 메시징 대기열에서 본격적인 이벤트 스트리밍 플랫폼으로 빠르게 발전했습니다.
><img data-action="zoom" src='{{ "assets/images/kafka-service.png" | relative_url }}' alt='absolute'>


## 쉽게 생각해보기

- Kafka는 실시간 이벤트 기반 애플리케이션 개발을 가능하게하는 오픈 소스 분산 스트리밍 플랫폼이다.

| ![이해하기 위한 그림]({{ "assets/images/01.png" | relative_url }})|
|:--:|
| *이해하기 위해 만든 이미지* |

> 이벤트가 발생하면 worker1,worker2,worker3이 어떠한 작업을 수행해야한다.  
> 위의 그림과 같이 이벤트가 발생하면 카프카 브로커로 메시지를 보내고
> worker1,worker2,worker3는 이벤트에 대해서 감시하고 있다가   
> 이벤트가 발생하면 해당 작업을 수행합니다.
> 
> 예를 들면...
> 피자가게를 예를 들어보겠습니다.
>> 1. 홀 직원이 피자,파스타,음료 주문을 받습니다.(이벤트 발생)
>> 2. 주방으로 주문을 전달합니다. (카프카 브로커 전달)
>> 3. 주방에서 직원들은 주문알림기계(카프카브로커)를 보고있습니다.  
      주문이 들어왔다는것을 확인합니다.
>> 4. 피자제조, 파스타제조, 음료제조를 각자 임무를 수행합니다.
> 
>각자의 임무에 대해서 서로에게 지장을 주지 않습니다.  
>중요한 부분중 하나라고 생각하는것이 서비스간의 느슨하게 결합이고 생각합니다.  
>(이러한 아키텍처를 활용한다면, 마이크로 서비스를 늘리는데에 부담이 줄어 들것같습니다.)

## 카프카에는 어떤 개념들이 있을까?

-------------
카프카를 간단하게 아래와 분류해 보았습니다.(간단하게만 적었습니다..)
1. Zookeeper
   - 주키퍼, Kafka cluster node의 상태, Kafka topic, partition 등을 관리합니다.
1. Broker 
   - 브로커, 프로듀서로 전달 받은 메시지를 저장합니다 and 컨슈머에게 메시지를 전달합니다.
1. Producer
   - 프로듀서, 브로커로 메시지를 전달합니다.
1. Consumer
   - 컨슈머, 브로커로 부터 토픽(이벤트)를 전달받아 받습니다.   
     브로커가 컨슈머에게 전달하는것은 아니고, 컨슈머가 토픽을 감시하고 있는 형태입니다.
1. Topic
   - 토픽, 이벤트라고 보면됩니다.

이외에도 partition,offset,replication factor,consumer group,cluster,Kafka Connect,Kafka Stream 등등 알아 볼것이 많습니다!  


이상 오늘 공부한 내용!
끗~

----------

#### <참조링크>  
[카프카 웹 사이트](http://kafka.apache.org/)  
[real-time-stream-processing-with-apache-kafka-part-1](https://dzone.com/articles/real-time-stream-processing-with-apache-kafka-part-1)
