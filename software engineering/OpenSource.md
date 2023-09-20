<div align=center>
  <h1> OpenSource 😺 </h1>
</div>

> 발표일　　|　 2023.09.20 <br />
> 발표자　　|　강준영 <br />

<div align=center>
  <h3>📇 목차 </h3>
</div>

[1. 정의](#🏭-정의)<br />
[2. 특징](#🌊-특징)<br />
[3. 방법](#🦴-방법) <br />

<br>

# 🏭 정의

#### 오픈 소스

```
소스 코드를 공개해 누구나 특별한 제한 없이 그 코드를 보고 사용할 수 있는 오픈 소스 라이선스를 만족하는 소프트웨어
```

<br>

# 🌊 특징

- 누구나 코드를 수정하고 공유할 수 있음

- 글로벌 협업이 가능

- 지식 공유와 집단적 혁신으로 전체 커뮤니티에 도움이 됨.

## 오픈 소스의 원칙

### 1. 커뮤니티

- 오픈 소스 커뮤니티는 공통의 목표를 달성하기 위해 모인 사람들의 모임.
- 공통의 가치와 목표가 의사 결정과 오픈 소스 프로젝트를 이끔

### 2. 투명성

- 커뮤니티의 모든 사람이 자신의 최고의 작품을 만드는 데 필요한 정보와 자료에 액세스할 수 있음.

### 3. 공개 협업

- 개인이 혼자서는 해결할 수 없는 문제를 그룹이 해결할 수 있음.

- 다른 사람들이 나중에 필요에 따라 솔루션을 수정할 수 있도록 규칙을 설정할 수 있음.

### 4. 신속한 프로토타입 제작

- 오픈 소스 프로젝트는 팀원들이 자주 프로토타입을 만들고 공유하는 반복적 접근 방식을 따름.

- 효과가 있는 변경 사항을 개선 및 수행하고 그렇지 않은 변경 사항은 폐기할 수 있음.

5. 포용적 능력주의

- 다양한 관점과 대화를 장려

- 합의에 따라 결정을 내리지만 성공을 우선시하며 최고의 아이디어는 커뮤니티로부터 더 많은 지지를 받음.

<br>

# 🦴 방법

```
maintainer는 해당 프로젝트의 로드맵과 디자인 원리에 준수한 코드만 승인을 합니다.

그래서 각 오픈 소스 프로젝트에 있는 Contribution Guide를 준수해서 작성해주세요.
```

### 1. Create an issue

```
코드를 작성하기 전에 issue를 작성하여 maintainer들과 토의를 해주세요.
```

### 2. Create a draft PR

```
모든 PR이 maintainer의 승인을 받는것은 아닙니다.
PR은 reasonably, small, focused 속성을 가져야 합니다. (코드 리뷰 용이)
하지만 작성한 코드의 양이 굉장히 클 수도 있습니다.
그래서 PR은 세부사항을 분리해서 올려야하는데,
한 기능안에 유기적으로 연결이 되어 있다면
PR만 보고 maintainer가 이해할 수 없으므로 PR을 reject 할 수 있습니다.

이를 방지하기 위해 방대한 코드를 draft PR로 먼저 올려서 maintainer와 소통 후 PR을 올리는걸 추천합니다.
```

### 3. Create a commit

```
draft PR에서 쪼갠 내용을 PR로 올립니다.
각 프로젝트 별로 지켜야 할 다양한 Commit Convention이 존재합니다.
(ex : signed-off message)
이를 준수하지 않으면 CI 단계에서 자동으로 reject 됩니다.
```

### 4. Check code format locally

```
commit 뿐만 아니라 Code Convention도 존재합니다.
로컬 환경에서 점검 후 PR을 작성합시다.
안그러면 어차피 CI에서 막혀요.
```

### 5. Create a PR

```
description을 통해 PR을 요약해주세요.
maintainer는 해당 description을 보고 review를 진행할겁니다.
프로젝트 별로 다르지만, 각각의 PR은 최소 두명 이상의 리뷰어가 승인을 해야 통과합니다.

description도 4단어를 넘지 않으면 CI에서 reject 합니다.
```

### 6. Request review

```
리뷰 과정에서 리뷰어를 append 할 수 있습니다. Maintainer는 리뷰어로 요청을 하지 않더라도 리뷰가 가능합니다.
```

### 7. Update per feedback

```
리뷰어의 요청에 따라 코드를 변경할 수도 있습니다.
이러한 커밋은 첫번째 커밋에 스쿼쉬 될것이므로 signed-off 메세지를 포함시키지 말고 full description을 작성하지 마세요.
```

<br>

#### 출처

1. 오픈 소스란 무엇인가요? : https://aws.amazon.com/ko/what-is/open-source/

2. How to Contribute : https://github.com/Samsung/ONE/blob/master/docs/howto/how-to-contribute.md
