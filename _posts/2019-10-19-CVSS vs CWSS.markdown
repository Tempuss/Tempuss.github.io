---
layout: post
title: CVSS vs CWSS
date: 2019-10-19 00:00:00 +0900
category: BoB  
---
## 아래 글은 BoB 8기의 Terrarium 팀의 산출물 일부 입니다.


애초에 CWSS에서 CVSS를 따와서 만들었다고 할정도로 거의 유사함


* CVSS는 취약점 자체에 대한 평가(취약점의 기술적 부분, 보고서, exploit 코드등)에 대해서 더 많이 다루고
  CWSS는 취약점의 impact에 대해서 좀더 자세하게 다룸
  
  
  
  
|Metric|CVSS v2 Value|CVSS v3 Value|Comment|Comment|
|------|------|------|------|------|
|매트릭|	base, Temporal, <br>Environmental|	Base Finding, <br>Attack Surface, <br>Environmental|	2단계로 구분 /<br>1단계(Confidentiality,Integrity,<br>Availability) / <br>2단계 (Access vector, Access complexity,<br> Authentication)|	Base, Temporal,<br> Environmental|
|스코<br>어링<br>방식|고정적<br>(정해진 입력값만으로<br>계산)|가변적<br>(계산시 담당자가<br>임의에 값을 넣어서<br>유동적인 계산을 할 수<br> 있음)|	고정식|	고정식|
|계산<br>벡터|base score의 벡터만 <br>자주 쓰임(AV:AC:PR:UI:S:C:I:A)|	base, Attack, <br>Environment 모두 쓰임<br>(TI:AP:AL:IC:FC:RP:RL:<br>AV:AS:IN:SC:BI:DI:EX:EC:P)|	모든 계산 백터를 사용. <br>단, 2단계 계산으로 1단계 벡터의 값이<br>큰 영향을 미침.|	base score를 주로 보는건 <br>cvss와 동일하지만 RVSS만의<br> 벡터와 공식이 존재함<br>(AV:AC:PR:UI:Y:S:C:A:I:H)|
|계산<br> 시기|	취약점이 이미 발견되었을때 사용가능|	일부정보가 알려지지 않았어도<br>(취약점 발견&확인이 되지 않았어요)<br>일부 정보만 가지고<br>점수 계산 가능|	계산 시기 정보 없음.	|CVSS base 이기 때문에 취약점이<br> 이미 발견되었을떄 사용가능|
|피해<br> 측정|	기밀성,무결성, 가용성 만으로 피해를 추산함|	기술적 영향도, 권한,<br>발생빈도등 더 다양한<br>요소를 고려하여 추산함|	시스템 영향도를 주 평가<br> 요소로 고려하고, 취약점에 대한<br> 평가를 부수적인 평가<br> 요소로 고려함.|	Robot이 물리적/시간적/의존적으로 갖는<br> impact에 대해서 보다 상세하게 추산함|
|주요<br> 평가<br> 요소|	취약점의 특징(exploit, 기술적 난이도등)|	취약점의 impact에 비중을 둠|	취약점이 시스템에<br> 미치는 영향을 주로 고려함|	3rd 파티 라이브러리에 대한 <br>고려와 취약점 발표 이후의 시간에 따른 고려,<br> 물리적인 안전에 영향을 끼치는 벡터까지 고려함|