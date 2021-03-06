---
layout: post
title:  "Front-End 프로젝트의 Test Code 작성 경험기"
# categories: experience
tag: [ test ]
---


코드스쿼드에서 (배민찬 사이트 디자인을 참고해) vanilla js로 만든 프론트엔드 프로젝트를 진행했었고, 마지막 미션으로 테스트 코드를 작성해 보기로 했다.  
<br>
처음 작성해 보는 테스트 코드라 시행착오가 많이 있었고, 누적된 노하우가 없어서 고민할 거리가 많았던 경험이었다. 테스트는 이론보다 경험을 잘 누적해 두는 게 중요하다는 크롱의 조언이 생각나서 글로 정리해 놓기로 마음먹었다.

<br>

## 공부 순서

- 1: 테스트 환경 구성
  - 사용할 라이브러리 검색, 호환성 체크 및 환경 구성, 테스트용 폴더 구조 구성
- 2: (테스트라는 환경에 들어가기 위한) 최소한의 테스트 이론 공부
  - 주요 키워드 파악이 목적
- 3: 라이브러리 기초 익히기
  - 공식 문서 + 구글 검색
- 4: 테스트 코드 작성 + 공부 (오픈 소스 테스트 코드 벤치마킹, 그때그때 필요한 내용) + 이슈 메모
  - ⇒ 이 단계부터는 위의 3가지를 계속 반복했다.

<br>

## 테스트 환경구성과, 결과물 먼저...

* Unit Test (메인 테스트)⇒ test.html을 만들고 node server로 라우팅하여, 브라우저에서 확인
  * mocha.js (test framework)
  * chai.js (assertion library)
  * sinon.js (test double library)
* E2E Test (이건 가볍게 경험) ⇒ node.js로 확인
  * testcafe (e2e node module)

<div style="background: #eee; border-radius: 5px; padding: 20px; text-align: center;">
  <em style="font-size: 0.9em;">[unit] helpers.test.js (유틸 메서드 모음)</em>

  <img src="https://user-images.githubusercontent.com/23192677/44468605-8b5d0300-a660-11e8-906d-ee805bc65e1a.png" alt="helpers.test.js 결과화면" width="60%">
  <br>

  <em style="font-size: 0.9em;">[unit] AutoCompleteSearcher.test.js (자동완성검색 UI)</em>

  <img src="https://user-images.githubusercontent.com/23192677/44598298-8093a100-a80d-11e8-9253-bae5039395ad.png" alt="AutoCompleteSearcher.test.js 결과화면" width="60%">
  <br>

  <em style="font-size: 0.9em;">[e2e] autoCompleteSearcher.test.js</em>

  <img src="https://user-images.githubusercontent.com/23192677/44468655-adef1c00-a660-11e8-9f95-0be8286d71a0.png" alt="autoCompleteSearcher.test.js 결과화면-01" width="60%">
  <img src="https://user-images.githubusercontent.com/23192677/44468670-b3e4fd00-a660-11e8-9180-580215cf15bd.png" alt="autoCompleteSearcher.test.js 결과화면-02" width="60%">
</div>

<br>

<br>

## 테스트 주요 키워드 파악하기

처음에는 라이브러리를 먼저 공부하려 했으나 자꾸 생소한 용어가 나와서 찾아 보니 **소프트웨어 테스트 분야에서 통용되는 용어**라는 것을 알게 되어 키워드 파악을 목적으로 공부를 했다.  

<br>  

주요 키워드는 아래와 같았다.

- 유닛 테스트=단위 테스트(unit test), 통합 테스트(integration test), E2E 테스트
- 테스트 프레임워크, 단언문(assertion), 테스트 커버리지(test coverage), 테스트 더블(test double, spy, stub), 테스트 케이스(test case)

<br>

<br>

## 테스트 코드 설계 및 규칙 정의하기

테스트 코드를 작성하다 보니 실제코드를 로직을 보지 않고도 명세와 테스트 타겟의 속성명, 메서드명 만으로도 잘 읽혀야 하기에 개발이라기보다 문서를 코드로 작성한다는 느낌이 들었다.  

그렇기 때문에 **가독성, 특히 일관성 있는 코드 구조**가 필요하다고 생각되어 아래와 같이 **나만의 규칙들을 세우고 테스트 코드를 일관성 있게 작성해 보려 했다.** 이렇게 되면 실제코드의 수정이 일어날 때나 테스트 에러가 발생했을 때, **어디서 무엇을 고쳐야 하는지 빨리 파악하고 대응할 수 있어 유지보수에도 좋을 거라 생각**했다. (실무에서도 경험해 봐야겠지만..)

<br>

### 1. 시각적/기능적으로 읽기 쉬운 구조로 테스트 그룹짓기

테스트 코드 작성을 시작할 때 오픈소스인 TOAST UI의 테스트 코드를 많이 참고 했는데, 처음에 가장 눈에 띈 것이 일관성 있는 구조로 테스트 코드를 묶어 관리하는 것이어서 벤치마킹을 해보았다.  

<br>

내가 설계한 구조는 아래와 같다.

- 최대한 3뎁스를 지켜서 구성
  - 대제목(객체명) → 소제목(# 분류) → 테스트케이스
  - 3뎁스 이상 들어가면 가독성이 떨어질 것이라 판단했다.

```javascript
/* 대제목 */
describe('객체명 또는 파일명', () => {
  /* 소제목 */
  describe('# 분류 (유사한 역할끼리)', () => {
    /* 테스트 케이스 */
    it('테스트 내용 설명', () => {
      // given
      // when
      // then
    });

    context('일부 테스트들이 반복되는 상황(when, ~할 때)을 서술할 경우, 한번 더 묶어줄 수도 있음', () => {
      it('테스트 내용 설명', () => {
        // given
        // when
        // then
      });

      it('테스트 내용 설명', () => {
        // given
        // when
        // then
      });
    });
  });

  describe('# 분류 (유사한 역할끼리)', () => {
    //...
  });

  //...
});
```
<br>

### 2. 소제목은 '#분류명'으로, 분류 기준은 유사한 성격끼리

- helpers.js : 독립적인 함수들을 모아놓은 객체라 간단히 메서드명으로 분류해 봤다.
- AutoCompleteSearcher.js : UI Component 객체라 유사한 역할을 하는 메서드끼리 분류해 봤다.
  - \# Create (Instance 생성 테스트) / \# Initailize (Instance 초기화) / \# Storage / \# Request / \# Rendering / \# UI / \# Event
  - ⇒ (실제코드의 메서드 선언 순서와 유사하기도 함)

테스트 코드를 작성하고 난 후, MVC 프로젝트 테스트 코드를 작성하는 친구와 대화를 나눴었는데 (내 프로젝트와 비교할 때) 객체들의 역할과 관계가 달라서 인지, 나의 테스트 경험으로 얘기하기 어려운 부분들이 있음을 알게 되었다. 또 객체의 역할이 무엇인지에 따라 테스트 작성 목적이 달라지고 분류가 달라지겠구나를 느꼈고, 객체의 역할이 뚜렷해야 좋은 테스트 코드도 만들 수 있겠구나 했다.

<br>

### 3. 유사한 테스트 끼리 묶은 그룹 안에서 (describe, context) 공통으로 사용하는 given을 변수와 hook메서드를 활용해, 테스트 코드의 given중복을 없애고 가독성을 높이기

항상 테스트 코드의 (given, when, then 에서) given이 제일 길어지곤 했는데, 그럴수록 테스트 코드가 잘 읽히지 않았다. 그런데 그룹을 먼저 지어 놓고 그 안에 테스트 코드를 작성해 나가다 보니, **유사한 성격으로 묶은 그룹이기 때문에 전제조건 또한 유사해서 given이 계속 비슷하게 작성됨**을 발견하였다. 

그제서야, 이전에 다른 코드에서 보았던 **hook메서드(before, beforeEach, afterEach, after)나 상위 그룹핑 공간에 정의한 변수들을 어떤 기준으로 분리** 했는지 이해할 수 있었다.  

- hook메서드: before, beforeEach, afterEach, after 등. 각 scope마다 테스트 케이스 호출 전후로 실행할 코드를 컨트롤 해준다. (이런 종류의 메서드는 mocha뿐만 아니라 다른 테스트 프레임워크에서도 유사한 이름으로 제공하는 것 같다.)

그래서 기존에 작성했던 테스트 코드들을 변경해 봤다. 중복되는 given을 가진 테스트 코드를 묶은 그룹핑 공간에서 given을 전역변수처럼 공유하고 hook메서드에 반복되는 행위를 기재했더니, **테스트 코드 안에서는 복잡했던 given 중복이 사라져서 훨씬 더 읽기 쉬운 테스트**가 되었다.  

<br>

적용한 예

- instance 객체를 매 테스트 마다 새로 만들기 ⇒  beforeEach 사용
  - (그래야 각 테스트가 서로 영향받지 않고 동일한 Instance에서 테스트되는 것이 보장될 수 있다.)
- 최근에 저장된 검색어가 이미 있을 경우를 테스트 할 때 ⇒ beforeEach 사용
  - (가짜 최근 검색어를 활용하여 Storage에 저장하는 행동이 반복되므로 상위 그룹핑 공간에서 정의하고 테스트 전에 미리 반복 실행되도록 함.)

<br>

### 4. 테스트 더블 객체를 효율적으로 쓰되, 테스트되지 않은 메서드는 별도 테스트하기

UI Component 객체 안에서 구성한 메서드들은 **각기 다른 수준으로 추상화** 되어있고, 하위레벨의 메서드는 상위레벨의 메서드 안에서 호출되는 식으로 의존하고 있다. 가장 낮은 하위레벨 메서드는 다른 메서드를 의존하지 않아 테스트가 간단하지만, **상위로 갈수록 다른 메서드를 의존해 구성되는 경우가 많아서 테스트를 하기가 어려웠다**. 책을 읽어 보니 이럴 때 테스트 더블을 쓰면 된다고 해서 써 보았다.

나는 여러가지 종류를 써 보지는 않고 아래의 2가지를 주로 사용했다.

- spy : 스파이를 심어 놓고 몰래 확인하는 것처럼, 원래 메서드가 실행된 후에 호출정보(호출횟수, argument, return값)를 받아 보고 싶을 때
- stub : 원래 메서드를 덮어씌워 대신 실행되는 함수를 만들 수 있음. return도 가짜로 보내줄 수 있다.

또 책에서는 테스트 더블을 남용하지 말고 꼭 필요한 곳에서 사용하는게 좋고, 깨지기 쉬운 테스트가 되지 않기 위해 주의해야 한다고 하던데 이게 잘 이해가 되지 않았다. **어떻게 주의해야 할까? 고민하다가 테스트 더블 중 stub을 사용해서 실제코드가 호출되지 않은 메서드에 한해 별도로 테스트를 진행하는 것이 좋겠다고 판단**하였다.  
그러다 보니 생각보다 많은 테스트 더블을 코드에서 사용하게 되었는데, 이후 [이 글](https://midojeong.github.io/2018/04/19/mocking-is-a-code-smell/)을 읽고 (사실 너무 어려워 다 이해하지 못했고 뉘앙스만 얻었음) 테스트 더블을 줄이는 방법에 대한 고민이 좀 더 필요하겠구나 생각했고 이건 일단 숙제로 남겨 두기로 했다. -0-

<br>

### 5. 기타 자잘하게 세운 규칙들...

- 먼저 테스트 코드를 작성했던 친구의 1:1 코드 리뷰 시간에 슬쩍 같이 참여해 보면서 가장 크게 남았던 메시지는, 테스트 코드를 작성하는데 있어서 **실제코드의 목적을 제대로 테스트 했는지가 가장 중요**하다는 것이었다. 그래서 테스트 코드를 작성할 때 **실제코드를 항상 옆에 두고 먼저 목적을 읽은 다음 테스트 코드를 짜라고 조언**해주셨다. 이것을 나의 테스트 코드 작성 내내 지키기 위해 노력했다.
- given, when, then 패턴 유지하기
- **given이 길어지는 경우가 많아서, 종류별로 순서**를 정해 두는 것도 도움이 되었다.
  - dummy data 정의 → test double 객체 정의 → dom 객체나 instance 객체속성 셋팅
- **명세의 내용을 테스트 코드가 번역한다는 느낌으로 작성** 하기.
  - 잘 짠 테스트 코드를 읽어 보면서, 명세의 내용이 그대로 테스트 코드로 바뀌는 것처럼 자연스럽게 읽힌다는 것을 느꼈다.
  - 그래서 명세를 적고 코드를 작성한 뒤 서로가 잘 매치되어 읽히는지 읽어보았다.
- 명세는 개발자보다 **사람이 이해하기 좋은 스토리**로 쓰는 것이 테스트하기 더 좋은 것 같았다.
  - 에러가 났을 때마다 명세를 보며 에러를 파악했는데, 개발 관점으로 쓰인 명세는 내가 코드를 머릿속에 항상 간직하고 있는 것이 아니기 때문에 이해가 빨리 되지 않았고, 명세의 개발키워드에 얽매여서 사고하다보니 에러를 판단하는 시야가 좁아지는 느낌이었다.
  - 지금 같은 작은 규모에서도 이런데, 큰 프로젝트에서 테스트를 돌릴 때는 코드를 다 숙지하고 있을 수 없고 그럴수록 상황과 문맥으로 설명하는 명세가 개발자에게 더 도움이 될 것 같다.
- 라이브러리를 쓰긴 하지만, **라이브러리 의존성을 낮추는 코드를 지향하려** 했다.
  - assertion 같은 경우, 똑같은 조건이어도 다양한 표현(문장)이 되게 제공하는데
  - 이것을 단일화하려고 노력했고, 사용하는 표현을 한정하여 단언문을 만들려고 했다. (to.equal, to.deep.equal, not.equal, to.be.true, to.be.false 이거면 거의 대부분의 단언문 작성이 가능했음)
  - 또 간단한 것은 native 메서드를 활용하기로 했다.
  ```javascript
expect(oAutoCompleteSearcher).to.be.an.instanceof(AutoCompleteSearcher); // 이것보다
expect(oAutoCompleteSearcher instanceof AutoCompleteSearcher).to.be.true; // 이렇게.
  ```

<br>

<br>

## 테스트 코드 작성 중 만났던 고민과 해결책

시간이 지나면 지금보다 더 좋은 해결책을 찾을 수도 있겠지만, 고민한 이유와 해결책을 찾아나간 과정을 기록해두는 것도 의미가 있을 거라 생각했다.

<br>

### Q. 추상화수준이 다른 메서드들을 어떻게 테스트 해야 효율적일까?

이 문제가 가장 큰 고민거리였고, 계속 수정을 거듭한 이유 중 하나 였던 것 같다.

helpers.js(유틸 모음 객체)는 메서드가 각각 독립적이라 Unit Test가 간단했으나, AutoCompleteSearcher.js(자동완성검색 UI Component 객체)는 여러 추상화수준으로 나뉜 메서드들이 한데 모여 부르고 불리는 구조라 **어떤 메서드 레벨에서 주도권을 쥐고 테스트를 해야 하는가?에 대한 판단**이 어려웠던 것이다.

<br>

- **(X) 처음 전략 : 추상화수준으로 구분**
  - 상위레벨 메서드 테스트 시 : 사용하는 하위레벨 메서드의 호출여부만 체크하고,
  - 하위레벨 메서드 테스트 시 : 해당로직을 진짜 테스트하자.
  - ⇒ 명세는 '검색어를 입력하면 검색목록이 열린다'라고 하는데 정작 assertion은 '목록열림' 호출을 체크하고 끝나니 명세와 코드가 맞지 않아 찝찝했다. 그러다보니 테스트 코드가 잘 안 읽히는 건 당연했다.
- **(O) 최종 전략 : 로직의 복잡한 정도로 판단**
  - 단순한 로직의 하위레벨 메서드는 : 상위레벨 메서드에서 한번에 테스트 (ex. dom classList 조작)
  - 복잡한 로직의 하위레벨 메서드는 : 상위레벨 메서드측에서 spy나 stub을 사용해 호출여부나 최종결과값만 체크하고 넘어가고, 하위레벨 메서드에 대한 상세한 테스트를 별도로 작성

<br>

(예) 검색창에 검색어를 입력하면, 결과목록이 나타난다.

- 상위레벨 메서드 테스트 측: inputEvent가 발생하고, 요청이 일어난 뒤, renderList()가 실행된다.
  - renderList는 복잡한 로직을 가진 하위레벨 메서드로 판단
  - 여기서는 응답데이터 갯수와 렌더링된 결과목록 갯수가 일치하는지만 확인
- 하위레벨 메서드 테스트 측 renderList():
  - 유효한 데이터들의 렌더링등을 상세하게 체크

<br>

### Q. requestAnimationFrame 테스트?

- **(X) 총 동작시간(재귀가 호출되는 횟수 * 1frame 호출시간) 이후 assertion 호출**
  - ⇒ 환경마다 시간차이가 발생할 수도 있고,
  - ⇒ 버퍼를 충분히 준다는 대안도 근본적인 해결책이 아닌 것 같아 다른 방법을 고민.
- **(O) Promise를 반환, 재귀가 끝나는 시점에 resolve**
  - ⇒ 테스트코트측에서는 async, await로 제어. await 이후 assertion 호출
  - 그러나 기존메서드가 Promise를 return하는 코드로 바꼈는데 이게 테스트를 위해 변경된 거라 (동작은 똑같이 잘 되지만) 더 좋은 코드로 개선된 건가? 하는 의문점이 들었다.

<br>

### **Q. 클라이언트측 템플릿 렌더링 테스트?**

- **(X) html string 비교**
  - ⇒ 탭이나 스페이스에 따라 스트링값이 달라지므로 비교 불가.
  - ⇒ 돔 구조나 속성 구성은 얼마든지 바뀔 수 있음. 안전하지 않다.
- **(O) dom list 전체 갯수, list 한 개의 주요 속성값 비교.**
  - ⇒ data-index, data-value, innerText 등등

<br>

### Q. (localStorage를 이용한) 최근검색어 저장 테스트?

- **(X) 네이티브 객체인 localStorage를 이용하여 테스트.**
  - ⇒ 브라우저 환경에서 테스트한다는 보장이 없고,
  - ⇒ 브라우저에 접근할 수 있어도, 매번 초기환경을 리셋해 둬야 하므로 불합리함
- **(O) 저장소를 temp객체 변수로 대체하고, 목적대로 잘 저장되는지 테스트**

```javascript
describe('# Storage', () => {
  let fakeStorageSpace;

  beforeEach(() => {
    fakeStorageSpace = {};

    // 브라우저 스토리지를 사용하지 않으므로, 동일한 메서드를 가진 fake객체로 대체
    oSearcher.oStorage = {
      getData(key) {
        return fakeStorageSpace[key];
      },
      setData(key, value) {
        fakeStorageSpace[key] = value;
      },
      isExpiredData(savedTime, savingDuration) {
        const currentTime = +new Date();
        const gap = currentTime - savedTime;
        return gap >= savingDuration;
      }
    };

    sinon.stub(oSearcher, '_checkStorageModule').callsFake(() => undefined);
  });

  // (생략)....
```
<br>

### Q. **이벤트 테스트?**

- **(X) handler 만 테스트**
  - ⇒ event 객체를 직접 만들어줘야 하는 불편함
  - ⇒ dom에 이벤트가 등록되었는지 별도 확인 필요
- **(O) new Event('click') + dispatchEvent 사용하여 이벤트 발생**
  - ⇒ 실제 dom에서 이벤트를 발생시키므로 위의 불편함이 해결된다.

<br>

<br>

## (테스트를 통한) 실제코드 수정사항

밸리데이션

- storage가 구조를 제안한 parentStorage를 상속받지 않았을 경우 에러를 throw하도록 수정 (_checkModule)
- 클래스 생성시 필수옵션인  wrapperElem이 없을 경우 에러를 throw하도록 수정
- 벨리데이션을 이상하게 하고 있던 부분이 확인되어 수정


코드 가독성

- 변수명: 목적이 명확하게 보이지 않는 이름을 많이 개선
- 메서드 선언순서 : 동작이 발생되는 순서로 일부 개선하여 코드파악을 쉽게 함


(언젠가는 문제가 될 수도 있었던) 티 안나던 기능실수 개선

- 자동완성 목록을 close하는 메서드가 중복되는 시나리오가 있다는 걸 알게 되어 개선함. (spy로 호출 횟수를 expect 하던 중)


기타 개선

- 스토리지 이름을 종류별로 (최근목록, 검색응답데이터) 받던 것을 --> 대표이름 하나만 받게 하고 내부적으로 두 개로 나눠 사용하게 하여 개발자를 위한 UX 개선


다행히 리팩토링을 많이 한 덕인지 함수를 더 쪼개야 하는 식의 리팩토링은 많이 없었던 거 같다.

일부 코드만 작업하였기 때문에, 모두 테스트한다면 다른 종류의 문제가 발견되어 리팩토링을 하게 될 수도 있을 거라는 생각도 했다.

<br>

## 느낀 점

- **구현 코드와 마찬가지로 테스트 코드도 설계 방식과 전략이 필요**함을 느꼈다. 이런 것은 상황이 다 다르다 보니 검색으로 찾기 어려웠는데, 이번 경험으로 그런 노하우가 조금 생긴 것 같아 이득이 되었다.
- 테스트 코드가 실패하거나 명세를 꼼꼼히 작성하면서, **내가 평소에 자주 하는 안 좋은 개발습관을 파악**할 수 있었다. (벨리데이션 고려를 많이 안하고 짜는 경향이 있다는 걸 발견)
- **좋은 구현 코드가 좋은 테스트 코드를 부르는 것 같다**. 왜냐면 테스트 코드는 구현 코드의 변수 이름으로 작성하고 행동을 유추해야 하니까 ⇒ 이름이 잘 읽혀야 하고 ⇒ 이름이 잘 읽힌다는 것은 한가지 목적으로 추상화가 잘 되었다는 의미이고 ⇒ 목적이 명확한 메서드는 테스트할 대상이 명확하므로 ⇒ 테스트코드를 짜기가 수월해지기 때문에..
- '클린 코드'라는 책의 테스트 챕터 내용을 누가 요약해서 git에 올려 놨길래 읽어 봤는데, (예전 같았으면 읽어도 무슨 말인지 이해하지 못했을 내용을) **이번 경험 덕분에 굉장히 동의하는 부분이 많게 느껴졌던 것**도 뜻밖의 즐거움이었다.

<br>

## 남은 고민과 다음 방향

- 이번에 작성한 테스트 코드는 실제 코드와의 의존성 (DOM의 구조나 Selector, 메서드명 등등)을 줄이는 방법에 대한 고민이 좀 많이 부족했던 거 같다. 의존성이 높으면 실제코드의 변경사항이 생길 때마다 테스트 코드에서 수정할 포인트도 늘어나서 유지보수가 힘들다 보니 결국 버려지는 테스트 코드가 될테니...
- 어떻게 해야 중복되지도 않고, 빠트리지도 않는 테스트 작성을 할 수 있을까? 에 대한 고민도 더 필요하고..
- 어느 정도까지 상세하게 테스트해야 할지 감 잡기가 아직 어렵다. 이것도 경험을 쌓아서 터득해야 할 것 같다.
- 통합 테스트 같은 것들은 아직 감이 안 잡힌다.
- 나중에는 TDD도 시도해 보고 싶다. (박미정님과 김훈민님의 TDD 실천기와 장점에 설득 당할 것 같..)

<br>

## References

- [책] [자바스크립트 테스트와 디버깅 1~4장](http://www.yes24.com/24/goods/11573621?scode=032&OzSrank=1)
- [글] [마이크로소프트웨어 393호 중 '자바스크립트와 TDD'](https://www.imaso.co.kr/archives/3408), [3년간의 TDD 인생 회고](http://huns.me/development/2206)
- [공식사이트 문서] mocha, chai, sinon
- [코드] [오픈소스 TUI Editor Test](https://github.com/nhnent/tui.editor/tree/master/test), 코드스쿼드 친구들이 작성한 테스트 코드, 기타 자료들의 예제
- ~~많은 시행착오 및 인내심~~

<br>
