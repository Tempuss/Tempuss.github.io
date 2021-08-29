---
layout: post
title: Apache Kafka 
date: 2021-05-20 00:00:00 +0900
category: Data-Engineering
---

### 정의

---

pub-sub 모델의 메세지 큐이며 분산환경에 특화되어 있다

### topic

---

메시지를 구분하는 기준 

각 토픽은 여러개의 파티션으로 나눠져서 저장되며 파티션내의 한칸을 로그라고 칭한다

각 데이터는 한칸의 로그에 순차적으로 append됨

이때 메세지의 상대위치를 나타내는게 offset임(배열의 인덱스)

![topic](/assets/img/kafka_topic.png)


파티션을 여러개로 둘 경우 메세지는 round robin  방식으로 저장됨

이때는 메시지가 순차적으로 소비되는것을 보장할 수 없다

### Producer

---

메시지를 생산하는 주체. 즉 카프카에 데이터를 밀어넣는 역할을 하는 존재를 producer라고 한다

### Consumer

---

메시지를 소비하는 주체 즉 producer가 카프카에 저장한 메시지를 가져가서 어떠한 연산 행위를 하며 메시지를 처리한다

이때 consumer는 스스로 처리량을 조절 할수 있다

consumer는 topic내 존재하는 파티션의 offset위치를 통해 이전에 마지막으로 접근했던 offset위치를 기억하기 때문에 Consumer가 장애가 나도 마지막 접근 위치에서부터 다시 읽을 수 있다

### Consumer Group

---

여러개 컨슈머의 그룹으로 하나의 토픽에 대한 책임을 가진다

컨슈머 그룹은 해당 topic의 파티션과 1:n 매칭을 해야 한다

보통은 파티션 개수와 컨슈머 개수를 맞추는것을 추천한다

컨슈머 그룹내의 한개의 컨슈머가 장애가 발생하면 해당 컨슈머 그룹이 rebalance를 통해 다른 컨슈머가 이를 이어 받아 처리한다

offset  정보가 저장되어 있기에 가능한일


![topic](/assets/img/kafka_offset_2.png)

### broker

---

카프카 서버를 지칭함

브로커 id에 대한 설정을 통해 동일한 노드내에 여러개의 브로커를 띄울수도 있다

### zookeeper

---

분산 메세지 큐의 정보를 관리해주는 소프트웨어

최근엔 주키퍼 없이도 카프카를 띄울수 있다

docker stats 모니터링

```json
docker stats --all --format "table {{.Container}}\t{{.CPUPerc}}\t{{.MemPerc}}\t{{.BlockIO}}" --no-stream >> stats.csv
```

- 참고 : [https://github.com/sparrc/containermon/](https://github.com/sparrc/containermon/)

[https://github.com/kafka-dev/kafka](https://github.com/kafka-dev/kafka)

참고

- [https://medium.com/@umanking/카프카에-대해서-이야기-하기전에-먼저-data에-대해서-이야기해보자-d2e3ca2f3c2](https://medium.com/@umanking/%EC%B9%B4%ED%94%84%EC%B9%B4%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0-%ED%95%98%EA%B8%B0%EC%A0%84%EC%97%90-%EB%A8%BC%EC%A0%80-data%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%9D%B4%EC%95%BC%EA%B8%B0%ED%95%B4%EB%B3%B4%EC%9E%90-d2e3ca2f3c2)
- [https://engineering.linecorp.com/ko/blog/how-to-use-kafka-in-line-1/](https://engineering.linecorp.com/ko/blog/how-to-use-kafka-in-line-1/)
- [https://engineering.linecorp.com/ko/blog/how-to-use-kafka-in-line-2/](https://engineering.linecorp.com/ko/blog/how-to-use-kafka-in-line-2/)
- [https://springboot.cloud/34](https://springboot.cloud/34)
- [https://ohjongsung.io/2020/01/04/카프카-튜닝-방안-정리](https://ohjongsung.io/2020/01/04/%EC%B9%B4%ED%94%84%EC%B9%B4-%ED%8A%9C%EB%8B%9D-%EB%B0%A9%EC%95%88-%EC%A0%95%EB%A6%AC)
- [https://heodolf.tistory.com/11](https://heodolf.tistory.com/11)
- [https://www.cloudkarafka.com/blog/part1-kafka-for-beginners-what-is-apache-kafka.html](https://www.cloudkarafka.com/blog/part1-kafka-for-beginners-what-is-apache-kafka.html)
- [https://ooeunz.tistory.com/115](https://ooeunz.tistory.com/115)
- [https://freedeveloper.tistory.com/353?category=909995](https://freedeveloper.tistory.com/353?category=909995)
