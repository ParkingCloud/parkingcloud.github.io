---
title: "[강의] 추천시스템(Recommendation System)"
description: "추천시스템을 이용해서 사용자의 취향을 파악해보자."
date: 2020-01-30 11:00:00
category: 기술
tags: [추천시스템, 무관심아이템]
author_profile: false
---
앱으로 음악을 들을 때면 '내가 좋아할 음악'과 같은 리스트가 제안되기도 하고, 옷을 쇼핑할 때면 내가 좋아하는 스타일의 옷이 제일 먼저 화면에 보여진다. 인스타그램 혹은 페이스북을 할 때에도 내가 관심있어할 만한 제품에 대한 광고나 재미있는 영상이 뜨기도 한다. 이렇게 '빅데이터'를 통해서 나의 취향을 파악하고 '추천시스템'을 통해서 나의 취향에 맞는 상품들을 제안받는다. 어떤 알고리즘을 가지고 나의 선호도를 반영한 추천 리스트가 뜨는지는 자세하게 모르지만, 무언가 '빅데이터 기반 추천 시스템'이 반영되었다는 것은 어렴풋이 느낄 수 있다.

NHN 외부 교육을 통해 듣게 된 김상욱 교수가 진행한 '추천시스템' 강연은 우리의 궁금증을 해결해 준다. 컴퓨터가 소비자의 취향을 어떻게 간파하고, 각자에게 알맞는 상품을 제공하는지에 대해 풀어낸다. 강연은 다음과 같은 목차로 추천 시스템의 기본 개념, 최신 기술, 응용에 대해서 설명하고, 머신 러닝 기술을 이용하여 추천 시스템을 어떻게 실현하는가에 대해서 설명한다.

```
[목차]
Recommendation Systems: An Overview
Concepts and applications
Collaborative filtering (CF)
Exploiting Uninteresting Items for Effective CF
Ratings setting
One-class setting
Some More Research Results
Recommendations
Graph engines
Conclusions
```

### 추천시스템
추천하고자 하는 대상(Active User)이 물품을 구입하면 추천 시스템을 통해 그 대상에게 아이템을 추천한다. 사용자에게 평점을 받은 후 그 데이터를 기반으로 추천하는데 활용된다. (ex. Amazon, Netflix)

### 추천시스템 기술
* Content-based Approach(컨텐츠)
* Collaborative Flitering Apporach(협업)
* Trust-based Apporach(신뢰)
* Hybrid Approach(결합)

### Content-based Approach
* Active User의 Content를 추출하여 Content끼리 비교한다.
* 주의할 점은, Active User의 취향으로만 비교하여 추천하고 다른 사람의 취향과는 비교하지 않는다.

### Trust-based approach
* Active User가 신뢰하는 사람은 취향도 존재한다.
  * 인간적 신뢰 X
  * 구매입장에서의 신뢰 O
* 즉, 취향 면에서 신뢰할 수 있는 관계가 필요하다.

### Collaborative Filtering(CF)
협업 필터링(Collaborative Filtering) 추천 기술은 사용자와 유사한 취향을 가진 사용자들을 찾고, 그들이 공통적으로 선호하는 아이템을 찾아 사용자에게 추천해주는 기술이다.

* 신뢰관계가 없어도 가능하다.
* Active User와 취향이 비슷한 사람이 높게 평가하는 아이템을 추천한다는 개념이다.
  * Active User가 잘 모르는 아이템에 몇 점을 줄 지 알아야 가능하다.(예측)
  * 점수가 제일 높은 아이템 몇 가지를 추천한다.

### 무관심 아이템 활용법
김상욱 교수는 협업 필터링 추천의 정확도를 높이기 위해 사용자의 무관심 아이템을 활용하는 법을 제안한다.
아래와 같이 분류되는 무관심 아이템에 대해서는 사용자가 매우 낮은 평점을 부여할 것을 전제로 한다.

* 무관심 아이템(Unrated items)
  * 사용자가 몰랐던 아이템
  * 사용자가 알았지만 별로 좋아하지 않아서 평점을 주지 않은 아이템(사용자의 부정적인 선호도 반영)

### 취향이 비슷한 사람을 찾는 법
* Rating Matrix를 이용한다.
  * 나하고 취향이 비슷한 사람을 찾는다.
  * 취향이 비슷한 사람들이 각 아이템에 준 데이터 통계를 작성한다.
  * 비슷한 취향에는 선호도 점수를 더 반영한다.

### 사용자의 선호도 분류
* 사용 전 선호도(Pre-use Preferences)
  * 아이템의 실제 내용이 아닌 meta-data(장르, 제목 등)에 의해 결정됌
* 사용 후 선호도(Post-use Preferences)
  * 아이템의 실제 내용에 의해 결정됌

### Hybrid approach
* 시너지를 얻기 위하여 여러 기술을 합친 시스템

---
추천시스템은 단순한 추천을 하는 것이 아니다. 사용자의 선호도를 적절히 반영하여 취향에 맞는 아이템을 추천하여 만족도를 높여가기에 구매욕구가 샘솟는 것이 아닐까? 파킹클라우드 제품들도 모든 사람들의 마음에 쏙 들어서 구매욕구가 샘솟게 해주세요!

[만족도 평가]
파킹클라우드: ★★★★★(5점/5점)
