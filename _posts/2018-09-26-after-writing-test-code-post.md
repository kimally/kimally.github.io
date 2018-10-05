---
layout: post
title: 'Test code 글이 여러군데 퍼진 그 후 - 얻은 것과 부작용'
tag: [ 잡담 ]
---

'[Front-End 프로젝트의 Test code 작성 경험기](https://lumiloves.github.io/2018/08/21/my-first-frontend-test-code-experience)' 라는 글이 내 생애(?) 처음으로 다수의 개발자들에게 공유되었던 (나에겐 아주 큰 의미의) 이벤트가 있은지 근 한 달이 지났다. 이 일로 인해 생각지도 못했던 것들을 얻었고, 부작용도 있었으며, 그동안 느낀 바가 있어 기록해두려 한다.

<br>

## 3일동안 접속자 수가 1000명을 넘었다! @_@

크롱을 통해 코드스쿼드 페이지에 공유된 것을 시작으로, 개발 페이스북 페이지인 '그날그날 프로그래밍', 'DEVLOG' 에도 게시되었고, OKKY사이트에도 올라가고, 내가 평소 팔로우하던 몇몇 개발자분들의 타임라인에도 공유되고, 또 모르는 많은 분들이 공유해가셨다.

아주 사적인 내용만 적고 있었던 블로그라 방문자가 기껏해야 하루 0\~5명 사이였는데, 게시된 27일부터 29일까지 3일간 누적 접속자가 1000명을 넘어섰다. 아래 그래프는 근 한달 간 블로그 접속자수 추이다. 페이스북이랑 OKKY에서는 적지만 아직까지도 조금씩 유입률이 있다. 요즘은 하루 평균 5\~15명 정도 유지되는 거 같다.

![image](https://user-images.githubusercontent.com/23192677/46088869-50fafe80-c1e8-11e8-9aba-c679e1f3e073.png)

이런 정보들은 모두 Google Analytics 덕분에 얻어냈다 (땡큐 구글). 막 공유되었을 당시엔 Analytics 앱을 열어서 실시간 접속자가 얼마나 있는지, 오늘은 몇 명이 들어왔는지 구경하는게 게임보다(게임 잘 안하지만) 재밌었다. '0';;

그리고 여태 겪어보지 못했던 참 생소한 감정이 들었었다. 공유된 첫째날은 이렇게 많은 사람들이 볼 줄 몰랐기에 당황했다. 글을 막 완성하고 나서는 나 스스로도 만족스러웠는데, 갑자기 밖으로 퍼져버리니까 내 글이 부끄러워졌다. (틀린 내용이 있을 수도 있는데... 어떤 사람들은 보고나서 이게 뭐야 라고 하지 않을까? 누군가 보기에는 굉장히 부족해 보일텐데.. 다시 읽어보니 왜 이렇게 허접해 보이지? 주로 이런 생각이 들었었다.) 둘째날부터는 그날그날 프로그래밍에서도 좋은 글이라고 추천해주시고, 공유도 계속 되길래 나쁘지 않구나 하고 신경 많이 안 쓰게 된 거 같다.

내가 이런 일이 너무 부끄러운 것 같다고 크롱에게 말씀드리니, '한번이 어렵지 괜찮아지더라' 라고 대답해주셨는데 정말 그렇더라 : )

<br>

## 얻은 것 하나. 생각의 전환점

이번 경험으로 생각의 전환점이 몇 가지 있었다. 
<br><br>

1\. 내가 개발자로서 노력하고 있는 방향이 올바른 방향이구나 **안심**되었다.
<br><br>

2\. 그동안 셀 수 없이 많은 개발자 분들의 글을 보며 도움을 받았는데, 나도 다른 개발자에게 도움되는 글을 쓸 수 있다는 것을 **'믿게'** 되었다.
<br><br>

3\. 앞으로도 꾸준히 개발하면서 만나는 **생각과 경험을 정리해 글을 쓰고 공유해야겠다**고 (쓸 땐 괴롭지만) 다짐했다. 나의 경험을 **글로 '완성'하는 것의 가치**와 **'공유'하는 일의 힘**이 생각보다 크다는 것을 느꼈기 때문이다.

사실 테스트 글을 처음엔 간단히 정리만 할 요량으로 readme.md 쓰듯 쓰려고 했는데, 그동안 여기저기 적어놓았던 메모들을 모으다 보니 양이 많아져서 글이 되었다. 나만 이해할 수 있게 적은 메모를 남이 보기에도 괜찮은 글로 바꾸는 과정이 예상보다 빡세서 중간에 '내가 왜 이 시기에 이걸 쓰고 있지?' 라고도 했다. 그렇게 약 일주일동안 괴로워하며 완성했다. (그렇게 다른 개발 블로그나 기술서적들을 보며 더욱 감사할 수 있는 아이가 되었다는 :D )

그동안 **글로 탄생하지 못하고 지나간 좋은 경험들**이 많아서 아쉬웠고, 결과물로 완성하고 안하고가 하늘과 땅 차이라는 걸 실감했다.

(덧 1. [통나무들을 쌓아두었다고 집이라 말할 수 있을까](http://theschoolofnews.com/archives/1351) 라는 글을 보았는데 딱 좋은 비유라고 생각했다.)

(덧 2. 자바스크립트를 잘하시는 프론트엔드 개발자들이 HTML/CSS에 고통받는 기이한(?) 현상을 많이 목격해서, 나는 디자인을 보고 어떤 생각의 흐름으로 HTML/CSS코드를 만들어내는지에 대해서도 내킬 때 써보고 싶다.)
<br><br>

4\. 아 참 그리고.. **리액션의 소중함**을 알게 되었다. ㅋㅋ

나의 퇴사하고 큰 변화 중 하나는 '**버스를 타면 기사님께 인사드리려 노력하는 것**'이다. 

한동안 나의 세상에 어쩌면 가장 큰 비중을 차지했던 '직장'이라는 곳을 벗어나서 살게 되니, 그 자리가 다른 것들로 채워지게 되었는데 대부분이 공기처럼 존재해서 특별히 인식하지 않던 주변의 것들이었다.

그 중 하나가 버스안의 인사다. 백조가 되고 시간부자가 되었기 때문에, 빠르게 도착하는 방법보다 편하게 가는 방법을 찾게 되고 그러다보니 버스를 자주 이용했다. 그러면서 알게 된 사실은, 생각보다 많은 버스기사님들이 승객들이 들어올 때 눈을 마주치거나 인사를 하신다는 거였다. 그리고 대부분의 승객들은 카드를 찍고 자리를 찾는다.

하루에도 수백 번 하는 일이 승객을 태우고 내리는 것일 텐데 (잘 받아주지도 않는) 인사의 제스쳐를 유지한다는 것이 대단해보였다. 나의 지난 4년 간의 직장생활동안 당연해서 무심해진 일에 어떤 것이 있었는지도 떠올려 보았다.

이따금씩 버스기사님의 존재를 인식하고 버스를 올라타며 인사를 건내시는 분들도 있었는데, 이런 생각 이후 단순한 인사 그 이상으로 보였고, 좋아보였다. 그래서 나도 하고 있다. (근데 의식하지 않으면 또 까먹고, 부끄러워서 못할 때도 있고 하다. 근데 인사해보면 생각보다 잘 받아주심.)

<br><br>

추상화(?)하여 정리하자면...

기존엔 세상을 바라보던 시선이 내 세계에 주로 있었다면, 요즘엔 내 주변의 세계에 더 머물러 보려 한다는 거다.

4번 소제목이 민망해 할 정도로 뜬금없는 소리를 길게 한 것 같지만 사실 같은 소리다. 개발자라는 직업이 매력있는 이유 중 하나가 같이 배우고 나눠주는 걸 즐거워하는 사람들을 쉽게 만날 수 있다는 것이라 생각하는데, 나는 주로 받는 포지션일 때가 많아 주는 사람들에게 익숙하고 무뎠다.

이번에 글을 공유하고 나서 접속자가 많아진 만큼 댓글이나 리액션도 기대했는데 댓글 1개와 하트 11개가 달려있다. (이렇게 갯수를 세어놓으니 엄청 쪼잔해보이..) 근데 여태껏 나도 많은 사람들의 시간과 노력이 들어간 수많은 글을 소비하고 리액션을 한 적이 있나 생각했을 때 진짜 없던 거 같다. 이제는 잘 본 글에는 하트 누르는 정도로 리액션을 하고 있다(댓글은 아직 부끄러워서). 그리고 '리액션이 큰 힘이 됩니다'라는 멘트는 뻥이 아니었다. 댓글이랑 하트, 그리고 공유해주신 분들 너무 감사.

참 당연해 보여서 놓치는 것들이 많다. 이렇게 하나씩 콩깍지가 벗겨질 때마다 까먹지 않으려고 해야지.

<br>

## 얻은 것 둘. 기회

메일로 입사 지원 제안을 몇 번 받았고 (나한테도 이런 일이..),

프론트엔드 컨퍼런스에서 발표 요청도 받았다. (나한테도 이런 일이...)

원래 나는 발표울렁증 같은게 있어서 대학교 때도 발표보다는 PPT만들기를 선호하던 애라 고민을 엄청 했는데, 조언자 세 분에게 조언을 구하니 다들 '안 할 이유가 없다'고 해서 하기로 했다. (근데 수락하고 난 다음 날부터 벌써 떨려서 우황청심환 사먹음)

발표자로 홈페이지에 올라가고 난 뒤 코드스쿼드 친구들, 전 직장에서 같이 일한 분들이 멋지다 축하한다 말을 많이 해주셨다. 근데 사실 지금은 이름만 올라갔을 뿐 아직 한 게 없는 지라.. 구직활동과 동시에 잘 준비해야지.

<br>

## 그치만 부작용도 있었다..!

개발블로그에 글을 꾸준히 올리기로 다짐한게 6월말인가 그렇다. 그때 나의 [글쓰기 초심](https://lumiloves.github.io/2018/06/26/TIL)에 대해 TIL에 남겼었다. 남을 위한 글을 쓰면 심리적 장벽이 높아지니깐 진짜 나를 위한 글쓰기로 하루 한 줄이라도 오늘 공부한 내용에 대해 글을 올리자고.

근데 테스트 글이 공유되고, 사람들이 계속 들어오니깐 의식하게 되더라. 한줄 두줄 짜리 막 쓴 글을 올리는게 좀 그래졌다.(이 글도 글감을 모으기 시작한지는 2주 정도 됐는데 쉽게 글로 완성하기가 어려웠다. 부작용.) 그래서 Github 잔디에 구멍이 나기 시작했다. 마음이 아프다. 잔디 심기가 은근 만족감을 주는데ㅠ

**나에게는 정성스럽게 잘 쓴 글도 중요하고, 남을 의식하지 않고 완성도 낮은 글을 쓰는 것도 중요하다.** 그래서 막 쓰는 글 / 정리된 글 두 가지 타입으로 페이지를 나눠 놓기로 결정했다. UI 작업을 곧 할 예정이다. (구상한 메뉴 ⇒ Dev, Log(timeline), Tag, About)

<br>

## 계속 묵묵하게 하자.

테스트 공부를 하고 글을 완성하면서도 그랬듯이 뭔가 하나 끝내면, 후련함과 동시에 다음 해야 할 것이 또 기다리고 있다. 개발 공부를 깊히 하려고 하면 할수록 내가 모르는 것이 너무 많다는 걸 알아서 좌절한 적도 한 때 있었다.

근데 계속 하다 보니 내가 어느 위치에 있는지, 얼마나 했는지 보다는 어떤 태도를 유지하고 있느냐에 무게중심을 두고 묵묵히 계속 나아가는게 나에게 더 필요한 일임을 알았다.

거의 다 쓰고 보니 글 하나 공유한 일로 너무 많은 의미부여를 한 것인가? 하는 부끄러움(무슨 부끄러움이 이리 많은지)이 살짝 들지만 무시하고 글을 올리겠다. 근래 굉장히 와 닿았던 글귀가 적힌 이미지를 마지막으로 글을 마무리 한다.

![image](https://user-images.githubusercontent.com/23192677/46088987-869fe780-c1e8-11e8-9b31-4f21b06bd50e.png)
