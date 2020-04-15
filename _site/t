[1mdiff --git a/_posts/Programming/Knowledge/2019-12-30-this-is-what-good-codes-really-are.md b/_posts/Programming/Knowledge/2019-12-30-this-is-what-good-codes-really-are.md[m
[1mdeleted file mode 100644[m
[1mindex 3e21773..0000000[m
[1m--- a/_posts/Programming/Knowledge/2019-12-30-this-is-what-good-codes-really-are.md[m
[1m+++ /dev/null[m
[36m@@ -1,478 +0,0 @@[m
[31m----[m
[31m-layout: post[m
[31m-title: "내가 생각하는 '좋은 코드'란 바로 이런 것이다"[m
[31m-date: 2019-12-31[m
[31m-description: "일개 개발자 지망생이 생각하는 '좋은 코드'란 무엇인지 일장 연설을 늘어놓겠습니다."[m
[31m-img:  /knowledge/literal-value-logo.jpg[m
[31m-categories: [Programming, Knowledge][m
[31m-tags: [good_code, clean_code][m
[31m----[m
[31m-[m
[31m-## 0. Index[m
[31m-[m
[31m-> 1. [들어가며](#1)[m
[31m-> 2. [좋은 코드란 그리 간단하지 않다](#2)[m
[31m-> 3. [성능](#3)[m
[31m->    - 3.1. [개인적인 예들](#3a)[m
[31m->    - 3.2. [기타 성능이 중요할 수 있는 상황](#3b)[m
[31m-> 4. [재사용성](#4)[m
[31m->    - 4.1. [모듈성](#4a)[m
[31m->    - 4.2. [범용성](#4b)[m
[31m-> 5. [구조화](#5)[m
[31m->    - 5.1. [용어 정의: 구조화](#5a)[m
[31m->    - 5.2. [코드 단위의 구조화](#5b)[m
[31m->    - 5.3. [패키지 단위의 구조화](#5c)[m
[31m-> 6. [추상화](#6)[m
[31m->    - 6.1. [용어 정의: 추상화](#6a)[m
[31m->    - 6.2. [코드 단의 추상화](#6b)[m
[31m->    - 6.3. [프로그램 단의 추상화](#6c)[m
[31m-> 7. [가독성](#7)[m
[31m->    - 7.1. [변수 작명](#7a)[m
[31m->    - 7.2. [Coding convention](#7b)[m
[31m->    - 7.3. [사용자 고려](#7c)[m
[31m->    - 7.4. [기타: 주석과 여백](#7d)[m
[31m-> 8. [그래서 어쩌자고?](#8)[m
[31m-> 9. [마치며](#9)[m
[31m-> 10. [자료 출처](#10)[m
[31m-[m
[31m-[m
[31m-<br id="1">[m
[31m-[m
[31m-## 1. 들어가며[m
[31m-[m
[31m----[m
[31m-[m
[31m-나는 왜 블로그를 할까? 이 글을 쓸 생각을 하면서 문득 드는 생각이다. 처음엔 공부한 내용을 정리하고 또 다른 사람들과 공유하고 싶어서 시작했다. 그 순수한 마음에서 시작해 생각보다 블로그가 내 기준에서 사랑을 받으면서 왠지 더 많은 관심을 받을 주제들을 찾아 쓰게 됐다. 그렇다. 팔리는 글을 쓰기 시작한 것이다. 내가 특정 문제보다는 일반적인 주제의 포스트들을 찾아 쓰는 것은 일부분은 이런 이유도 있다.[m
[31m-[m
[31m-하지만 한편으로는 나 자신을 위해서 쓰는, 뭐랄까 도저히 안 쓰고는 못 배기겠는 주제들도 있다. 내가 정말 깊은 통찰을 느낀 인생의 경험들, 단순히 머리가 아닌 마음으로 이해하고 깨달아버린 지식들. 이런 주제들은 마음이 불러서 써야 한다. 보통 포스트를 너무 길게 쓰면 내용이 좋아도 외면 받는다. 하지만 이런 주제들은 외면 받을지라도 생각한 분량만큼 쓸 생각을 한다. 그래서 시간이 너무 소요되면 '이렇게까지 해야 하나'하는 생각이 들기도 한다.[m
[31m-[m
[31m-오늘 주제가 딱 그런 내용이다. 과연 **'좋은 코드'란 무엇일까?** 개발자라면 한번은 고민해볼법한, 아니 사실 여러 번 고민했어야 할 주제. **모든 상황에 적용되는 황금률 같은 정답은 없으나 상황에 맞는 정답을 만들어내는 주요 구성 요소들에 대한 내 고민의 결과들을 오늘 적어볼까 한다.** 정말로, 도대체, 대관절 '좋은 코드'란 무엇인가?[m
[31m-[m
[31m-**나는 선배 개발자를 만났을 때, 또 면접 보러 가서 말미에 '당신이 생각하는 좋은 코드란 무엇이냐'는 질문을 반드시 던진다.** 나보다 개발을 잘할테니 어떻게든 보고 배우기 위함이다. 지금까지 한 이십여명 물어본 것 같은데 참 반응들이 재밌다. 나름의 철학을 가진 사람도 있고, '읽기 좋은 코드'라고 무난하고 별 영양가 없는, 하지만 마냥 틀렸다고는 할 수 없는 정답을 말해주는 사람도 있고, 딱히 생각을 안 해봤는지 별다른 말을 못하거나 안하는 사람도 있다. 나의 이 글은 내 경험과 고민에서 비롯됐지만 이 분들의 영향도 결코 무시못한다. 그래서 이 글을 그분들께 바친다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-내용 구성은 먼저 **'좋은 코드 = 읽기 좋은 코드'가 아님을 살펴볼 것이다.** 가독성은 좋은 코드의 매우매우 중요한 부분이지만 좋은 코드를 구성할 수 있는 요소는 이보다 더 많을 뿐더러 가독성이라는 말 자체도 너무 추상적이기 때문에 이런 까다로운 질문에 대한 쉽게 도망가는 대답밖에는 안 된다. 우리는 더 깊게 갈 것이다. 더 넓고 깊게.    [m
[31m-**그 다음 장부터는 내가 생각하는 좋은 코드의 주요 판단 요소들을 살펴볼 것이다. 이들은 성능, 재사용성, 구조화, 추상화, 가독성 등 5가지로 추렸고, 각 장마다 요소의 보다 구체적인 요소들을 실제 예시와 코드를 통해 살펴볼 것이다.** 마지막으로는 이들을 고려해서 코드를 짜자는 개인적인 당부와 함께 글을 마치겠다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-들어가기 전 이것만큼은 이해해주길 바란다. 일단 코드는 전부 파이썬이고 난 현업 경험이 없어 예시로 드는 것들이 알고리즘이나 매우 간단한 코드일 수도 있다. 그리고 내용은 철저히 개인적인 주관에서 비롯되었고 비유나 설명을 위한 자료 조사는 하지만 이 로직과 구성은 이미 상당 부분 머릿속에 완성되어 있는 상태였다. 그래서 실력의 부족으로 누락된 중요한 요소, 논리의 모순, 내용의 어설픔 등이 있을 수 있는데 이는 댓글로 지적해주시면 깊이 고민해보겠다. 솔직히 말하면 내용이 어설플 것 같아서 벌써부터 자괴감이 들기는 한다.[m
[31m-[m
[31m-어쩌다보니 크리스마스 특집으로 쓰게 됐네. 그 전에는 써야겠지? 그래야 최근에 나온 영화 '아이리시맨'을 그날 볼 수 있을테니까.[m
[31m-[m
[31m-시작합니다.[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-<br id="2">[m
[31m-[m
[31m-## 2. 좋은 코드란 그리 간단한 문제가 아니다[m
[31m-[m
[31m----[m
[31m-[m
[31m-내가 선배 개발자들에게 '좋은 코드가 뭐라고 생각하세요?'라고 물어보면 십중팔구 **코드의 가독성**을 이야기한다. 거의 대부분이 가독성을 언급하는데 물론 좋은 대답이다. 우리는 본인이 폰 노이만이나 리누스 토발즈가 아닌 이상 회사에서 협업을 하게 될 것이고 거대한 시스템이나 기능의 일부를 함께 개발하기에 서로가 서로의 코드를 이해할 수 있어야 한다. 이런 이슈를 많이 겪을 현업인들에게 물어서 그런지 답변의 95% 이상이 가독성을 이야기하는 것은 이상하지 않고 **나도 가독성이 좋은 코드의  매우, 또는 가장 중요한 요소라고 생각한다.**[m
[31m-[m
[31m-하지만 첫 장에서 언급했듯이 **좋은 코드의 조건을 '가독성'에 한해서 이야기하는 것은 부적절하다.** 일단 내가 질문했을 때 5%의 사람들은 가독성 이외의 대답을 줬다. 가독성도 중요하겠지만 지금 자신들의 상황에서는 다른 요소가 더 중요하다는 것을 뜻한다.[m
[31m-[m
[31m-또한 **`가독성` 용어 자체가 너무 모호하며 기업 크기, 현재 개발 상황, 사업하는 도메인, 리드 개발자 성향 등에 따라 천차만별일 수 있다.** 이는 '정의', '진리' 등이 무엇이냐고 묻는 것과 비슷한 것으로 모두가 만족할 수 있는 정답같은 것은 없다.  [m
[31m-매우 간단한 예를 들어보자면 어떤 사람들은 주석이 없어도 잘 읽히는 코드가 중요하다고 생각한다. 이런 사람들은 주석을 최대한 피하는 것을 지향한다. 하지만 어떤 사람들의 말을 들어보면 적재적소의 주석을 매우 긍정적으로 생각하기도 한다. 좋은 코드에 대한 이런 이슈 등은 정말 오랜 토론의 대상이 되어 왔고, 개인적인 생각에 이는 정말 스타일의 차이로 밑의 가독성 장에서도 언급할 예정이다.[m
[31m-[m
[31m-![달의 위상 변화](/assets/img/knowledge/good_codes_moon.png)[m
[31m-[m
[31m-이 장을 쓰면서 `좋은 코드`에 대한 좋은 비유가 떠올랐다. **좋은 코드를 달에 비유할 수 있겠다.** 달은 다 알다시피 지구의 하나뿐인 위성으로 기상이 좋으면 거의 매일 볼 수 있는데 자체 발광하지 않고 태양의 빛을 반사해서 우리가 지구에서 볼 수 있다. 그래서 지구와 달, 태양의 위치에 따라 지구에서 보이는 달의 모습이 조금씩 달라진다. 그 모습을 위상(phase)이라고 하며 위 사진은 지구와 달, 태양의 위치에 따른 달의 위상 변화에 대한 이미지로 이 위상들은 우리에게 익숙한 보름달, 초생달, 그믐달 등의 용어로 표현되고는 한다.[m
[31m-[m
[31m-여기에 더해 다는 모르는 내용으로는 달은 지구를 중심으로 도는 공전주기와 자체 회전하는 자전주기가 같아 지구에서는 달의 한 쪽면만을 볼 수 있다. 다른 말로 하면 **우리가 지구에서 사는 이상 달의 뒷면은 결코 볼 수 없다는 것이다.**[m
[31m-[m
[31m-**좋은 코드는 달과 같다.** 우리는 새벽녘에 특유의 감성을 불어넣는 달을 사랑하며 좋은 코드인 달에 대해 모든 것을 알고 싶어하고, 또 알고 있다고 자부한다. 지구에서 달을 바라보며, 달이 명확히 시야에 보이기 때문에 '좋은 코드란 저런 것이다'라고 단정짓는 것이다. 이때 **우리가 볼 수 있는 달의 모습, 위상은 가독성을 상징한다. 가독성은 좋은 코드의 가장 중요하고 명확한 요소 중 하나이기 때문이다.**[m
[31m-[m
[31m-하지만 우리가 의식적으로 노력하지 않는 이상, **우리는 달의 온전한 모습을 보지 못한다. 과학이 발달하고 천문학자들의 노력이 있었기에 우리는 우리가 보는 달의 모습이 달의 전부가 아님을 안다. 위상이 곧 본체가 아니듯, 가독성이 곧 좋은 코드의 유일한 조건은 아닌 것이다.** 과연 달의 뒷면은 어떻게 생겼을까? 앞면과는 다른 특징이 있을까? 우리는 더 노력해야 한다. 좋은 코드의 다른 조건들도 더 탐구해봐야 하는 것이다.[m
[31m-[m
[31m-또한 우리가 보는 달의 모습 또한 시시각각 변한다. 이는 우리에게 너무 익숙하며 음력 달력은 이런 달의 위상을 기준으로 한다. 가독성의 모습 또한 상황에 따라 변할 수 있는 것. 이렇기에 지금 이 시점에 달을 손가락으로 가리키며 '달이란 과연 저런 것이다'라고 말하는 것은 어불성설이라 하겠다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-우리는 달에 대한 우리의 이해가 부족함을 깨달았고 이제 달의 뒷면을 조사할 것이다. 달의 뒷면은 무엇들로 구성되어 있는가? 그리고 지구에서 볼 수 있는 각 위상들도 마찬가지로 탐구 대상이다. 달은 반지름이 약 1700km에 달하는 매우 큰 천체로 쉽지만은 않을 것이다. 하지만 포기할 수 없다. 다음 장부터 본격적으로 살펴보도록 하자.[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-<br id="3">[m
[31m-[m
[31m-## 3. 성능[m
[31m-[m
[31m----[m
[31m-[m
[31m-내가 아는 한 컴공을 전공하는 모든 학생들은 `알고리즘` 수업을 듣는다. 알고리즘은 현실의 다양한 문제를 컴퓨터를 통해 해결하는 방법을 배우는데 이중 꼭 배우는 개념으로 `시공간 복잡도(time and space complexity)`가 있다. **복잡도는 문제를 해결하는 방법의 성능을 논하는 개념으로 단순히 문제를 해결하는 것뿐만 아니라 얼마나 효율적으로 이 문제를 해결하는지도 중요하다는 것을 의미한다.** 이중 성능의 표기법으로 모두가 아는 $$Big O Notation$$이 유명하며, 학교에서가 아니더라도 알고리즘을 조금만 배우면 이 성능 표기법은 다 배우기 마련이다. **성능의 두 척도는 시간과 공간으로** 시간은 이 알고리즘이 문제를 해결하는 데 대략 얼마나 시간이 소요되는지, 공간은 해결하는 데 메모리가 얼마나 소요될지를 논한다. 또한 현대 전산 과학에서는 공간 복잡도보다는 시간복잡도를 더 많이 이야기한다.[m
[31m-[m
[31m-**나같은 사람은 실제 대량의 트래픽을 다룬다는가 하는 현업 프로젝트 경험이 없고, 대신 알고리즘 문제만 주구장창 많이 풀었다보니 한때 성능이 좋은 코드의 가장 중요한 척도라고 생각했다.** 알고리즘 문제 연습 플랫폼들에서 비효율적인 알고리즘을 효율적인 알고리즘으로 바꾸어 문제를 통과하는 것을 보며 그 신화를 내적으로 강화했고 그외에는 생각하지 않았다.[m
[31m-[m
[31m-그러던 중 Alan이라는 사람을 만나 **좋은 코드의 다른 가능성을 알게 되었다.** 매우 기초적으로 '매직 스트링, 넘버를 피한다든가', '필요하다면 변수, 상수를 구분하라'와 같은 것들로서 아래 가독성 파트에서 다룰 것이다. 짧은 순간이었지만 그 가르침은 내 코드 인생을 바꿨으며 모듈화, 구조화 등에 대한 관심까지 이어진다. 그 형이 아니었으면 이 포스트는 만들어지지 않았을 수도 있다. 그 형께 이 자리를 빌어 진심으로 감사를 전한다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-**난 올해 처음 취업 시장에 조금씩 뛰어들면서 선배 개발자들에게 그 질문을 던졌을 때 `성능`을 언급하는 사람들이 거의 전무하다는 것에 놀랐다.** 솔직히 한 절반 정도는 성능을 이야기할 줄 알았다. 하지만 대부분이 가독성을 언급했고 그래서 검색창에 좋은 코드라고 검색했을 때 '성능'을 언급하는 포스트를 찾기 힘들다는 것이 전혀 놀랍지 않다.[m
[31m-[m
[31m-하지만 분명히 말하지만 **성능은 좋은 코드의 조건이 될 수 있다.** 아무리 하드웨어의 발달로 전산능력이 향상되고 메모리 용량이 커진다고 해서 성능 문제가 만사해결되는 것은 아니다. 시간과 공간 성능 중요도에 대해 개인적인 예들과 합리적인 코드 예로 살펴볼 것이다.[m
[31m-[m
[31m-[m
[31m-<br id="3a">[m
[31m-[m
[31m-### 3.1. 개인적인 예들[m
[31m-[m
[31m-첫 번째 예는 알고리즘 주식 거래 회사에 면접 보면서 깨닫게 됐다. 면접을 보고 말미에 면접관들에게 '좋은 코드가 뭐라고 생각하세요?'라는 익숙한 질문을 던졌다. 그중 한 분이 '좋은 코드는 상황에 따라 너무 달라서 뭐라 하기가 힘든데... 일단 저희는 **실시간으로 가격 등락에 따라 거래가 바로바로 이루어져야 하기 때문에 latency(요청과 응답 사이의 시간 지연)가 낮은 코드가 중요한 것 같아요.'**[m
[31m-[m
[31m-이분이 성능이 중요하다고 말한 첫 분이었다. 그때 난 느꼈다. **이 회사는 물론 가독성 많은 요소가 정말정말 중요하겠지만 이 회사의 특수성상 시간 성능이 Mission critical하다.** 애초에 시간 성능이 충족되지 않으면 사업이 지속가능하지 않은 것이다. 아마 이 회사의 경우 코드의 가독성이 떨어진다고 해서 사업이 망하지는 않을 것이다. 그래서 가독성보다 성능이 더 중요한 예라고 하겠다. [m
[31m-[m
[31m-조금 다른 얘기로 난 면접이 끝나고 이 대답을 곰곰히 생각하면서 내가 수집하는 데이터가 조금 편향되었을 수 있겠다고 생각했다. 내가 면접을 본 곳들은 보통 실시간 어플리케이션을 다루는 곳이 아닌, 일반적인 기대 시간 안에 요청을 수행하면 되는 어플리케이션을 개발하는 곳들이었다. '특별한 철학이 있는 곳이 아닌 이상 이런 곳들이 좋은 코드에 대해 할 수 있는 말이 가독성 이외에 특별히 있을까?'하는 생각이 들기는 했다. 무시하는 것이 아니고 의도치 않게 요구사항이 무난한 곳에서만 면접을 보게 돼서 대답들이 편향되었을 수 있지 않을까 하는 것이다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-다른 예로는 파이콘에서 들은 이야기가 있다. 파이콘에서는 항상 라이트닝 토크라고 하여 현장에서 신청한 사람들에게 주제 상관없이 5분 간 발표를 할 수 있는 기회를 준다. 몇 년 전인지는 기억이 안 나지만 그때 라이트닝 토크에서 임베디드 프로그래밍을 하는 사람이 발표를 하면서 **자신이 개발하는 기기에는 일반 컴퓨터와 달리 메모리가 극히 제한적이기 때문에 코딩할 때 그 부분을 중점으로 둔다고 했다.** 이 또한 성능이 극히 중요할 수 있는 예라고 하겠다. 위의 예가 시간 성능이었다면 이 예는 공간 성능이 중요한 상황.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-위와 같은 예가 결코 개발하는 상황의 절대다수라고 말할 수는 없을 것이다. 하지만 위와 같은 상황이 얼마든지 존재하고 따라서 가독성을 좋은 코드의 절대 조건이라고 말하는 것은 힘들어 보인다.[m
[31m-[m
[31m-[m
[31m-<br id="3b">[m
[31m-[m
[31m-### 3.2. 기타 성능이 중요할 수 있는 상황[m
[31m-[m
[31m-성능 관련 장을 기획하면서 괜찮겠다고 생각한 몇몇 상황이 있다. 위의 예시가 내가 직접 경험한 것이라면 이 절의 두 예는 알고리즘 적으로 일리가 있다고 생각하는 것들을 가져왔다.[m
[31m-[m
[31m-먼저 순차탐색과 이진탐색. 이진탐색은 알고리즘을 조금 공부해보면 고생하게 되는 주제로 정렬된 1차원 배열에서 특정값이 어느 인덱스에 위치하고 있는지를 찾는 알고리즘을 말한다. 다 알다시피 이진(binary)라는 이름이 붙은 것은 원하는 값이 나올 때까지 배열을 절반으로 가르면서 탐색을 진행하기 때문이다. 따라서 이진탐색의 시간복잡도는 $$O(logN)$$이 된다. 반대로 순차탐색은 배열을 말 그대로 순서대로 훑으면서 값을 찾는데, 한 번 탐색할 때마다 탐색할 배열의 크기가 절반이 아닌 1이 줄어들기 때문에 시간복잡도는 $$O(N)$$이 된다. 시간복잡도상 이진탐색이 순차탐색에 비해 절대 우위에 있다.[m
[31m-[m
[31m-하지만 성능이 아닌 이슈로 넘어가보면 어떨까? 정렬된 배열 _arr_ 에 대해 특정값 _v_ 를 찾는 순차탐색, 이진탐색의 코드는 각각 다음과 같다.[m
[31m-[m
[31m-[m
[31m-```python[m
[31m-# 순차탐색[m
[31m-def sequential_search(arr, v):[m
[31m-    for i, n in enumerate(arr):[m
[31m-        if n == v:[m
[31m-            return i[m
[31m-```[m
[31m-[m
[31m-```python[m
[31m-# 재귀함수를 사용한 이진탐색[m
[31m-def binary_search(arr, v):[m
[31m-    def search(lo, hi):[m
[31m-        if lo == hi:[m
[31m-            return lo[m
[31m-        mid = (lo + hi) // 2[m
[31m-        if arr[mid] >= v:[m
[31m-            return search(lo, mid)[m
[31m-        else:[m
[31m-            return search(mid+1, hi)[m
[31m-[m
[31m-    return search(0, len(arr))[m
[31m-```[m
[31m-[m
[31m-각 탐색을 무난하게 구현했다. 이때 성능이 아닌 가독성의 측면에서 보자. 그러면 **순차탐색이 이진탐색에 비해 압도적으로 가독성이 좋은 것을 알 수 있다.** 애초에 순차탐색은 프로그래밍을 처음 배우는 사람도 반복문과 조건문만 배우면 짜볼 수 있는데 반해 이진탐색은 알고리즘을 조금 공부해본 사람도 버그 없는 코드를 짜기 어렵다. 실제로 버그 없는 이진탐색 코드는 1962년에야 작성되었으며 이진탐색은 취업면접에서도 낼 수 있는 수준의, 마냥 쉽지 않은 알고리즘이다.[m
[31m-[m
[31m-**그럼에도 위와 같은 문제상황이라면 백이면 백 이진탐색 알고리즘을 쓸 것이다.** 가독성이 순차탐색에 비해 안 좋지만 성능이 압도적으로 좋기 때문이다. 특히 배열의 크기가 크다고 해보자. 가령 배열의 크기가 10억 정도 된다고 할 때 순차탐색은 최대 10억번의 탐색을 해야하지만 이진탐색은 30번 정도($$log_210^9$$)면 된다. 30과 10억은 정말 말도 안 되는 차이기 때문에 이 정도 크기가 되면 누구나 이진탐색을 쓰지 않을까? 코드가 어렵다고 탓할 것이 아니라 이쯤되면 '내가 어떻게든 이해해볼게'가 될 것이다. 즉 **가독성을 성능이 찍어누를 수도 있다는 것.**[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-다음 경우는 페이스북을 보면서 생각이 들었다. 페이스북은 유저와 유저가 친구를 맺을 수 있으며 이런 소셜 네트워크는 그래프 자료구조로 표현하기 딱 알맞은 자료구조다. 각 유저를 노드 또는 정점(vertex)로 두고 친구 관계가 링크 또는 엣지(edge)가 되는 것이다. 이때 모든 유저의 집합을 V, 모든 친구관계의 집합을 E라고 하자. 그래프 자료구조를 구현하는 방법은 크게 두 가지인데, 하나는 `|V|`개의 인접 배열을 사용하는 방법과 `|V|`개의 인접 리스트를 사용하는 것이다.(`| |`는 안의 집합의 크기를 구하는 연산자로 간주하자) 각각의 구현은 서로를 보완하는 장단점을 갖는데 여기서는 공간만 이야기해보자. **인접 리스트를 사용하는 방법은 $$O(\|V\|+\|E\|)$$의 공간복잡도가 소요되고 인접 행렬은 $$(\|V\|^2)$$만큼의 공간복잡도가 소요된다.** 이 내용들은 그래프를 처음 배울 때 기본으로 익히고 시작하는 것들이다. **우리가 이 친구 관계를 그래프로 표현해야 할 때, 어떤 구현방법을 선택할지는 유저 집합 V와 친구 관계 집합 E의 크기에 따라 고려할 수도 있을 것이다.**[m
[31m-[m
[31m-공간만 고려했을 때는 일반적으로 두 구현 중 E가 V에 비해 지나치게 작은 희소 그래프(sparse graph)일 때는 인접 리스트를 사용하고, 관계가 충분히 많은 밀집 그래프(dense graph)일 때는 인접 행렬을 사용하는 것이 유리하다. 그 이유는 공간복잡도만 봐도 알 수 있는데 그래프가 희소하다는 말은 E의 크기가 작다는 뜻으로 이때 사용되는 공간은 $$O(\|V\|+\|E\|)$$로 그 반대에 비해 사용 공간이 훨씬 절약될 수 있기 때문이다. 반면 E의 크기가 V의 크기에 비해 그리 작지 않거나 더 많을 수 있는 밀집 그래프의 경우에는 공간복잡도상 그리 차이가 나지 않으면서 추가적으로 특정 연산에서의 시간성능 향상을 기대할 수 있다.[m
[31m-[m
[31m-자, 그럼 우리가 페이스북 CTO라고 해보자. 친구 관계는 페이스북의 핵심 기능이기 때문에 이 친구 관계를 그래프 자료구조로 표현하는 일이 매우 중요하다. 여기서는 follow 등은 신경쓰지 말고 오로지 친구를 맺는 기능만 생각한다. **문득 생각할 때 두 그래프 구현 중 어떤 구현이 페이스북의 친구 그래프를 표현하기에 적합할까?**[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-작년 자료를 보니 페이스북의 월간 활성 사용자수는 22억명이라고 한다. 편의를 위해 20억명이라고 하자. 물론 활성 사용자가 총 계정수는 아니지만 정확한 계정수를 파악할 수 없었기 때문에 약 20억개 이상의 계정이 존재하고 편의상 20억이라고 잡자. 이때 이 20억명의 집합이 V가 되며 \|V\|가 20억이 된다. 다음은 E를 추정해보자. 당신에게 묻는다. 당신이 페이스북 계정이 있다면, 등록된 친구수는 몇 명인가? 통계 자료에 의하면 페이스북 유저들의 평균 친구수는 338명이라고 한다. 중위수는 200명으로 이는 소수의 유저들이 친구수가 매우 많다는 것을 뜻한다.(한마디로 소수의 인싸들이 평균을 확 높이고 있다는 얘기)[m
[31m-[m
[31m-**중요한 것은 등록된 유저수에 비해 개인의 평균 친구수는 너무 적어서 이 그래프는 어떻게 표현해도 희소 그래프라는 것이다.** 인접 행렬 구현은 공간복잡도가 $$O(\|V\|^2)$$로 대략 $$4 * 10^{16}$$ 정도의 공간을 잡아야 한다. 반대로 인접 리스트 구현은 한 유저당 \|V\|만큼이 아닌, 평균적으로 338개의 공간이 필요하니 $$E$$의 크기가 대략 20억 * 338($$6 * 10^{10}$$)가 된다. 이때 공간복잡도는 $$O(\|V\| + \|E\|)$$로 1천억($$10^{11}$$)을 넘지 않기 때문에 이 경우에는 인접 리스트 구현이 더 유리한 것이 된다. **무엇보다 두 구현의 공간복잡도 차이가 너무 압도적이기 때문에 내 생각에 이 결정에 있어 성능을 결코 무시할 수 없는 것이다.** 따라서 이또한 성능이 좋은 코드의 중요한 요소가 될 수 있는 예라고 하겠다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-이처럼 내가 들은 실제 예와 충분히 고민 가능한 시나리오를 훑어보면서 **우리는 때로는 성능이 코드 결정에 중요한 역할을 할 수 있다는 것을 알게 됐다.** 면접을 보러 가서 '좋은 코드는 성능 좋은 코드입니다!'라고 말하는 것은 위험할 수 있지만 '좋은 코드의 조건 중에는 성능도 있다고 생각합니다'는 충분히 괜찮은 의견이 될 수 있을 것이다.[m
[31m-[m
[31m-이번 장이 좀 길어졌는데 다음 장부터 가독성 이전까지는 이보다 짧아지리라 기대한다.[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-<br id="4">[m
[31m-[m
[31m-## 4. 재사용성[m
[31m-[m
[31m----[m
[31m-[m
[31m-이 주제는 알고리즘으로 개발을 주로 하는 사람들, 나같은 사람들에게는 가장 낯선 주제다. 재사용성(reusability)이라. 재사용성은 당연하게도 한 번 작성했어도 다음 기회에 다시 사용할 수 있는 코드의 특징을 말한다. **재사용성이 낮은 코드는 특정 문제에만 지나치게 특화되어 비슷한 상황에서도 다시 쓸 수 없는 코드를 말하고 재사용성이 높으면 구체적인 값과 syntax는 달라도 비슷한 유형의 문제상황이라면 이 코드를 조금만 수정해 다시 사용할 수 있게 된다.** 이런 예를 곧 보게 될 것이다.[m
[31m-[m
[31m-알고리즘 문제를 푸는 사람들은 이런 재사용성을 전혀 신경쓰지 않고 코드를 짠다. 물론 그것이 이해는 간다. 당장 이 문제를 통과하면 이 문제를 당장 다시 보는 일은 없을 것이기 때문이다. 하지만 난 의아하게 생각한다. **현업에서 코드를 작성하고 다시 사용하는 일은 결코 없는 일일까?** 적어도 내가 들은 바에 의하면 그렇지 않다. SI 업체 같은 곳에서 선배가 짜놓은 코드를 세부사항만 수정하고 다시 쓰는 일이 꽤 있고, 프로그래밍이 아닌 재무쪽이지만 선배가 짜놓은 엑셀 파일을 매일 업무에 활용하는 경우도 들을 수 있었다. [m
[31m-[m
[31m-느낀 바는 **재사용성 높은 코드를 적절히 활용하면 실제 창의적인 업무와 관련 없는 지루한 작업을 매번 재계산할 필요없이 시간을 절약하고 코드를 짤 수 있겠다고 생각했다.** 그리고 **재사용성 높은 코드의 중요한 특징을 두 가지 추렸는데 크게 모듈성과 범용성이 있겠다.**[m
[31m-[m
[31m-[m
[31m-<br id="4a">[m
[31m-[m
[31m-### 4.1. 모듈성[m
[31m-[m
[31m-**모듈성(modularity)은 파이썬의 모듈(module)에만 국한되지 않는 소프트웨어 공학적인 용어로서 하나의 기능 단위가 하나의 작업만 하는 것을 뜻한다.** 이는 리눅스 쉘 명렁어 프로그램들의 주요한 특징으로 리눅스 CLI에서는 복잡한 기능을 하는 하나의 함수가 아니라 여러 개의 단순한 기능을 하는 기능들을 파이프라이닝(pipelining) 등을 통해 조합해 더 큰 일을 하는 것을 지향한다. [m
[31m-[m
[31m-이렇게 하나의 프로그램을 보다 단순하게 만드는 모듈성이 지니는 가치는 재사용성과 직결된다. 생각해보자. 여러 작업을 동시에 하는, 복잡한 기능을 한 번에 처리하는 기능에 대한 요구사항이 정말 그렇게 많을까? 상식적으로 생각해도 처리하는 기능이 많으면 많을수록 점점 그 기능은 보다 특수한 상황에 적합한 용도의 프로그램이 되고 덜 일반적인 프로그램이 된다. 하지만 단순한 기능의 프로그램을 여러 개 만들고 그들을 조합해 큰 기능을 하게 만든다면 각각의 단순한 기능은 각각이 필요한 상황이 독립적으로 여럿 생길 수 있다. 즉 전체 재사용성이 증대되는 것이다.[m
[31m-[m
[31m-모듈성을 고려할만한 예제를 하나 준비했다. 최근에 푼 [알고리즘 문제](https://algospot.com/judge/problem/read/CHRISTMAS)로 두 가지 형태의 코드를 제시한다. **이 문제는 한 문제에서 두 가지의 부분문제를 동시에 풀 것을 요구했는데 두 부분문제를 한 기능 내에서 해결할 수도 있고, 각 부분문제를 독립적인 모듈로 만들어 이들을 조합해 전체 문제를 풀 수도 있겠다.** 순서대로 코드를 보자. 두 코드 다 정답을 반환하기는 한다.[m
[31m-[m
[31m-[m
[31m-모듈성 낮은 코드:[m
[31m-[m
[31m-```python[m
[31m-from collections import Counter[m
[31m-[m
[31m-MOD = 20091101[m
[31m-[m
[31m-[m
[31m-def solve_two_problems(doll_boxes, K):[m
[31m-    cumul_dolls = [0][m
[31m-    for doll in doll_boxes:[m
[31m-        cumul_dolls.append((cumul_dolls[-1] + doll) % K)[m
[31m-[m
[31m-    # 1. Count total number of ways to buy dolls[m
[31m-    counter = Counter(cumul_dolls)[m
[31m-    total_ways = 0[m
[31m-[m
[31m-    for way in counter.values():[m
[31m-        if way >= 2:[m
[31m-            total_ways += way * (way - 1) // 2[m
[31m-[m
[31m-    total_ways %= MOD[m
[31m-[m
[31m-[m
[31m-    # 2. Maximum number of consecutive buys[m
[31m-    ret = [0] * len(cumul_dolls)[m
[31m-    prev = [-1] * K[m
[31m-[m
[31m-    for i in range(len(cumul_dolls)):[m
[31m-        if i > 0:[m
[31m-            ret[i] = ret[i-1][m
[31m-        else:[m
[31m-            ret[i] = 0[m
[31m-[m
[31m-        loc = prev[cumul_dolls[i]][m
[31m-        if loc != -1:[m
[31m-            ret[i] = max(ret[i], ret[loc] + 1)[m
[31m-[m
[31m-        prev[cumul_dolls[i]] = i[m
[31m-[m
[31m-    max_buys = ret[-1][m
[31m-[m
[31m-    return total_ways, max_buys[m
[31m-```[m
[31m-[m
[31m-모듈성 높은 코드:[m
[31m-[m
[31m-```python[m
[31m-def ways_buying(p_gifts, K):[m
[31m-    MOD = 20091101[m
[31m-    counter = [0 for _ in range(K)][m
[31m-    ret = 0[m
[31m-[m
[31m-    for i in range(len(p_gifts)):[m
[31m-        counter[p_gifts[i]] += 1[m
[31m-[m
[31m-    for i in range(K):[m
[31m-        if counter[i] >= 2:[m
[31m-            ret = (ret + ((counter[i] * (counter[i] - 1)) // 2)) % MOD[m
[31m-    return ret[m
[31m-[m
[31m-[m
[31m-def max_buys(p_gifts, K):[m
[31m-    ret = [0 for _ in range(len(p_gifts))][m
[31m-    prev = [-1 for _ in range(K)][m
[31m-[m
[31m-    for i in range(len(p_gifts)):[m
[31m-        if i > 0:[m
[31m-            ret[i] = ret[i-1][m
[31m-        else:[m
[31m-            ret[i] = 0[m
[31m-[m
[31m-        loc = prev[p_gifts[i]][m
[31m-        if loc != -1:[m
[31m-            ret[i] = max(ret[i], ret[loc]+1)[m
[31m-        prev[p_gifts[i]] = i[m
[31m-[m
[31m-    return ret[-1][m
[31m-```[m
[31m-[m
[31m-두 코드는 정확히 같은 일을 한다. 두 가지의 부분문제를 결국 풀어낼 것이다. 첫 번째는 한 함수를 짜서 이 블락 안에서 두 문제를 모두 해결하며 두 번째는 각 부분문제마다 함수를 작성해서 최종적으로는 두 함수를 조합해 문제를 해결한다. 여기서 로직은 안 봐도 된다. 두 코드 중 어떤 형태가 바람직하다고 보는가?[m
[31m-[m
[31m-**내가 볼 때는 두 번째 코드가 훨씬 바람직하다고 본다.** 그 이유는 다음과 같다.[m
[31m-[m
[31m-* **각 기능에 대해 함수 단위로 뚜렷하게 구분되어 있어 가독성이 증대된다.**[m
[31m-  - 재사용성이 높은 코드는 가독성도 좋기 마련이다. 사실 이 포스트의 각 장은 조금씩 얽혀있는 부분이 있다.[m
[31m-* **증대된 가독성 아래에서 필요한 문제 상황에 맞게 각 모듈을 필요할 때에 각각 사용할 수 있다.**[m
[31m-  - 앞서 말한 재사용성 높은 코드의 특징으로서 두 가지 부분기능 중 한 가지 기능만 필요할 수 있다. 이때 뚜렷하게 구분되어 있어 필요한 부분만 긁어가 바로 적용할 수 있다. 첫 번째 코드에서도 하려면 그렇게 할 수 있는데 각 영역 구분이 두 번째 코드처럼 뚜렷하지도 않고 잘 작성하지 않으면 두 가지 기능이 얽혀 이들을 분해해내기 매우 어려워질 수 있다.[m
[31m-* **기타로서 변수명 등을 작성하기 더 쉬워진다.** 결과 가독성이 추가로 증대된다.[m
[31m-  - 첫 번째 코드 블락의 함수는 두 가지 일을 하기 때문에 이름 짓기가 까다롭다. 자신이 하는 일을 다 이름에 담으면 지나치게 길어지기 때문이다. 하지만 두 번째 코드에서는 각각의 기능을 따로 담았기 때문에 좀더 기능에 집중해 작명할 수 있다.[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-결론은 **적재적소에 모듈성을 살린 기능 및 코드들은 전체 코드의 재사용성을 증대시키며 가독성까지 증대시키는 효과를 갖는다.**[m
[31m-[m
[31m-[m
[31m-<br id="4b">[m
[31m-[m
[31m-### 4.2. 범용성[m
[31m-[m
[31m-범용성 또한 재미있는 주제다. **범용성(generality)은 완전히 같은 프로그램을 보다 다양한 수요의 입력에 대응할 수 있도록 하는 코드의 특성을 이야기한다.** 범용성 또한 코드의 재사용성과 관련된 중요한 요소다.[m
[31m-[m
[31m-범용성은 위보다 더 좋은 예제가 하나 있다. 바로 Fizzbuzz 문제로 숫자를 입력 받아 1부터 N까지 수를 순회하면서 3의 배수일 때는 'Fizz', 5의 배수일 때는 'Buzz', 15의 배수일 때는 'FizzBuzz'를 출력하도록 하는 문제다. 원래 이 문제는 북미에서 아이들이 나눗셈을 학습할 때 하는 미니게임 같은 것이라고 하는데 알고리즘을 처음에 학습할 때도 유용하게 해보는 문제기도 하다.[m
[31m-[m
[31m-순회하는 상환 N을 100이라고 할 때 코드는 다음과 같겠다.[m
[31m-[m
[31m-```python[m
[31m-for n in range(1, 101):[m
[31m-    if n % 3 == 0 and n % 5 == 0:[m
[31m-        print('FizzBuzz')[m
[31m-    elif n % 5 == 0:[m
[31m-        print("Buzz")[m
[31m-    elif n % 3 == 0:[m
[31m-        print('Fizz')[m
[31m-    else:[m
[31m-        print(n)[m
[31m-[m
[31m-1[m
[31m-2[m
[31m-Fizz[m
[31m-4[m
[31m-Buzz[m
[31m-...[m
[31m-```[m
[31m-[m
[31m-정말정말 무난한 Fizzbuzz 코드다. 아마 당신이 초심자로서 파이썬을 공부하면서 이 코드를 작성했다면 아마 칭찬을 들었을 것이다. 하지만 분명히 하자. 우리는 초심자로서 칭찬 듣자고 이 포스트를 보고 있지 않다.[m
[31m-[m
[31m-지금 이 코드는 범용성이 매우 낮은 코드다. 이유는 분명하다. 왜 나눗셈을 3과 5만 진행하는가? 4, 7, 11 등도 나눗셈을 할 수 있는 것 아닌가? 또 왜 'Fizz', 'Buzz' 같은 단어를 출력하는가? 한국 사람인 나는 3으로 나눠질 때는 '울그락', 5로 나눠질 때는 '불그락'을, 15로 나눠질 때는 '울그락불그락'을 출력하고 싶을 수도 있는 것이다.[m
[31m-[m
[31m-이런 문제상황이 현실세계에는 다분하다. 우리가 어떤 서비스를 운영할 때 수많은 유저들의 요구사항은 천차만별이기 마련이기 때문이다. 즉, **여러 다양한 요소들과 함께 범용성 높은 코드를 작성하는 것도 중요하다.** 만약 위와 같이 다양한 수요를 충족하는 FizzBuzz 코드를 작성한다면 보다 다양한 나눗셈 수요를 충족할 수 있을 것이고, 학생들은 나눗셈을 더 잘하게 될 것이다.[m
[31m-[m
[31m-이런 코드를 작성해보자.[m
[31m-[m
[31m-[m
[31m-```python[m
[31m-def scalable_fizzbuzz(n, items=((3, 'Fizz'), (5, 'Buzz'))):[m
[31m-    N = len(items)[m
[31m-[m
[31m-    def generate(n, i, tmp_str):[m
[31m-        if i == N:[m
[31m-            return tmp_str if tmp_str else n[m
[31m-[m
[31m-        divisor, word = items[i][m
[31m-[m
[31m-        if n % divisor == 0:[m
[31m-            ans = generate(n, i+1, tmp_str+word)[m
[31m-        else:[m
[31m-            ans = generate(n, i+1, tmp_str)[m
[31m-        return ans[m
[31m-[m
[31m-    return generate(n, 0, '')[m
[31m-[m
[31m-[m
[31m-N = 200[m
[31m-length = len(str(N))[m
[31m-for i in range(1, N+1):[m
[31m-    # Python string formatting: 다수의 출력을 깔끔하게 처리하기 위해 사용함.[m
[31m-    print(f'{i:<{length}} : {scalable_fizzbuzz(i, ((2, "짝"), (5, "오호라"), (7, "럭키세븐"))):<20}', end='')[m
[31m-    if i % 3 == 0:[m
[31m-        print()[m
[31m-[m
[31m-1   : 1                   2   : 짝                   3   : 3                   [m
[31m-4   : 짝                  5   : 오호라               6   : 짝                   [m
[31m-7   : 럭키세븐            8   : 짝                   9   : 9                   [m
[31m-10  : 짝오호라            11  : 11                   12  : 짝[m
[31m-```[m
[31m-[m
[31m-보다 범용적인 FizzBuzz 기능을 함수로 만들었다. 다시 말해 모듈로 만들었다. 이 함수는 우리가 원하는 나눗셈 단위와 그때의 단어를 입력받을 수 있으며 난 어떤 수가 2, 5, 7로 나눠떨어질 때 각각 '짝', '오호라', '럭키세븐'의 단어를 붙여 출력하도록 했다.[m
[31m-[m
[31m-이 코드가 원래 Fizzbuzz 코드보다 어려운 것은 맞다. 하지만 분명한 것은 **이 코드가 범용성이 높은 코드로서 이 기능을 Customizate 할 수 있어 훨씬 더 많은 유저를 만족시킬 수 있는 것이다.** 그래서 만약 많은 유저가 사용하는 코드 또는 제품을 만들고 싶다면 이렇게 범용성을 고려한 코드를 짜야할 수도 있다.[m
[31m-[m
[31m-<br>[m
[31m-[m
[31m-정리하면 코드의 재사용성 또한 좋은 코드의 한 요소일 수 있고, 재사용성을 구성하는 주요 요소는 모듈성과 범용성이다. 모듈성은 한 기능(함수, 클래스) 등이 한 가지의 작업만 하도록 하는 것이고 이는 코드 전체의 재사용성을 높이고 보통 가독성에도 득이 된다. 다른 요소로는 범용성으로 범용성이 높은 코드는 같은 작업을 하더라도 보다 다양한 사용자의 수요를 널리 만족시킬 수 있어 자기만족 이상의, 사람들이 실제로 사용하는 프로그램의 중요한 요소가 된다.[m
[31m-[m
[31m-[m
[31m-<br>[m
[31m-<br id="5">[m
[31m-[m
[31m-## 5. 구조화[m
[31m-[m
[31m----[m
[31m-[m
[31m-<br id="5a">[m
[31m-[m
[31m-### 5.1. 용어 정의: 구조화[m
[31m-[m
[31m-[m
[31m-<br id="5b">[m
[31m-[m
[31m-### 5.2. 코드 단위의 구조화[m
[31m-[m
[31m-<br id="5c">[m
[31m-[m
[31m-### 5.3. 패키지 단위의 구조화[m
[31m-[m
[31m-[m
[31m-[m
[31m-[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## .[m
[31m-[m
[31m----[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## .[m
[31m-[m
[31m----[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## .[m
[31m-[m
[31m----[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## .[m
[31m-[m
[31m----[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## .[m
[31m-[m
[31m----[m
[31m-[m
[31m-[m
[31m-<br id="">[m
[31m-[m
[31m-## . 자료 출처[m
[31m-[m
[31m----[m
[31m-[m
[31m-* [달 한쪽만 보이는 이유? 우연 아냐 - Sciencetimes](https://www.sciencetimes.co.kr/?news=%EB%8B%AC-%ED%95%9C%EC%AA%BD%EB%A7%8C-%EB%B3%B4%EC%9D%B4%EB%8A%94-%EC%9D%B4%EC%9C%A0-%EC%9A%B0%EC%97%B0-%EC%95%84%EB%83%90)[m
[31m-* [페이스북 사용자 22억…유튜브와 위챗은? - KBS NEWS](http://news.kbs.co.kr/news/view.do?ncd=4029990)[m
[31m-* 『알고리즘 문제 해결 전략』27장 '그래프의 표현과 정의', 구종만, 인사이트(insight)[m
[31m-* [Unix philosophy - Parkito's on the way](https://shoark7.github.io/programming/knowledge/unix-philosophy-intro)[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-* []()[m
[31m-[m
[31m-컴퓨터엔지니어를 위한 기술 영어작문[m
[1mdiff --git a/_site/category/insight.html b/_site/category/insight.html[m
[1mindex ded7a64..3b71820 100644[m
[1m--- a/_site/category/insight.html[m
[1m+++ b/_site/category/insight.html[m
[36m@@ -257,6 +257,10 @@[m
 			<hr>[m
 			[m
 				<p class="category-item">[m
[32m+[m					[32m<a href="/insight/rationality/inform-to-my-subscribers">극소수 블로그 애독자들에게 고함</a>[m
[32m+[m				[32m</p>[m
[32m+[m[41m			[m
[32m+[m				[32m<p class="category-item">[m
 					<a href="/insight/rationality/way-to-employment">[시(詩)] 취업행(就業行)</a>[m
 				</p>[m
 			[m
[1mdiff --git a/_site/category/insight/rationality.html b/_site/category/insight/rationality.html[m
[1mindex aeac51e..7b41235 100644[m
[1m--- a/_site/category/insight/rationality.html[m
[1m+++ b/_site/category/insight/rationality.html[m
[36m@@ -228,6 +228,10 @@[m
 [m
 		[m
 			<p class="category-item">[m
[32m+[m				[32m<a href="/insight/rationality/inform-to-my-subscribers">극소수 블로그 애독자들에게 고함</a>[m
[32m+[m			[32m</p>[m
[32m+[m[41m		[m
[32m+[m			[32m<p class="category-item">[m
 				<a href="/insight/rationality/way-to-employment">[시(詩)] 취업행(就業行)</a>[m
 			</p>[m
 		[m
[1mdiff --git a/_site/category/programming.html b/_site/category/programming.html[m
[1mindex ca42ebf..504e86e 100644[m
[1m--- a/_site/category/programming.html[m
[1m+++ b/_site/category/programming.html[m
[36m@@ -229,10 +229,6 @@[m
 			<hr>[m
 			[m
 				<p class="category-item">[m
[31m-					<a href="/programming/knowledge/this-is-what-good-codes-really-are">내가 생각하는 '좋은 코드'란 바로 이런 것이다</a>[m
[31m-				</p>[m
[31m-			[m
[31m-				<p class="category-item">[m
 					<a href="/programming/knowledge/what-is-literal-evaluation-and-value">literal, evaluation and value</a>[m
 				</p>[m
 			[m
[1mdiff --git a/_site/category/programming/knowledge.html b/_site/category/programming/knowledge.html[m
[1mindex 320df41..c816ad5 100644[m
[1m--- a/_site/category/programming/knowledge.html[m
[1m+++ b/_site/category/programming/knowledge.html[m
[36m@@ -228,10 +228,6 @@[m
 [m
 		[m
 			<p class="category-item">[m
[31m-				<a href="/programming/knowledge/this-is-what-good-codes-really-are">내가 생각하는 '좋은 코드'란 바로 이런 것이다</a>[m
[31m-			</p>[m
[31m-		[m
[31m-			<p class="category-item">[m
 				<a href="/programming/knowledge/what-is-literal-evaluation-and-value">literal, evaluation and value</a>[m
 			</p>[m
 		[m
[1mdiff --git a/_site/index.html b/_site/index.html[m
[1mindex 29f0c59..40fac39 100644[m
[1m--- a/_site/index.html[m
[1m+++ b/_site/index.html[m
[36m@@ -224,23 +224,17 @@[m
 	[m
 	<article class="post">[m
 		[m
[31m-			<a class="post-thumbnail" style="background-image: url(/assets/img//knowledge/literal-value-logo.jpg)" href="/programming/knowledge/this-is-what-good-codes-really-are"></a>[m
[32m+[m			[32m<a class="post-thumbnail" style="background-image: url(/assets/img//insight/letter-to-my-subscriber-logo.JPG)" href="/insight/rationality/inform-to-my-subscribers"></a>[m
 		[m
 		<div class="post-content">[m
[31m-			<h2 class="post-title"><a href="/programming/knowledge/this-is-what-good-codes-really-are">내가 생각하는 '좋은 코드'란 바로 이런 것이다</a></h2>[m
[31m-			<!--<p>0. Index[m
[32m+[m			[32m<h2 class="post-title"><a href="/insight/rationality/inform-to-my-subscribers">극소수 블로그 애독자들에게 고함</a></h2>[m
[32m+[m			[32m<!--<p>1. 저의 근황[m
 [m
 [m
[31m-  [m
[31m-    들어가며[m
[31m-    좋은 코드란 그리 간단하지 않다[m
[31m-    성능[m
[31m-      [m
[31m-        3.1. 개인적인 예들[m
[31m-        3.2. 기타 성능이 중요할 수 있는 상황[m
[31m-     ...</p>-->[m
[31m-			<p>일개 개발자 지망생이 생각하는 '좋은 코드'란 무엇인지 일장 연설을 늘어놓겠습니다.</p>[m
[31m-			<span class="post-date">&nbsp;&nbsp;&nbsp;—&nbsp;2019, Dec 31&nbsp;&nbsp;&nbsp;—&nbsp;</span>[m
[32m+[m
[32m+[m[32m안녕하십니까? 정말 오랜만입니다. 2020년의 첫 포스트네요. 제 블로그에 극소수의 애독자가 있다는 것을 알고 있었습니다. 메일로 질문주시거나 한 분들이 있었거든요. 그때 참 뿌듯했는데요....</p>-->[m
[32m+[m			[32m<p>무소식이 희소식</p>[m
[32m+[m			[32m<span class="post-date">&nbsp;&nbsp;&nbsp;—&nbsp;2020, Feb 09&nbsp;&nbsp;&nbsp;—&nbsp;</span>[m
 			[m
 		</div>[m
 	</article>[m
[1mdiff --git a/_site/programming/knowledge/this-is-what-good-codes-really-are.html b/_site/programming/knowledge/this-is-what-good-codes-really-are.html[m
[1mdeleted file mode 100644[m
[1mindex 3a1ec80..0000000[m
[1m--- a/_site/programming/knowledge/this-is-what-good-codes-really-are.html[m
[1m+++ /dev/null[m
[36m@@ -1,843 +0,0 @@[m
[31m-<!DOCTYPE html>[m
[31m-<html lang="en">[m
[31m-<head>[m
[31m-	<meta charset="utf-8">[m
[31m-	<title>내가 생각하는 '좋은 코드'란 바로 이런 것이다 - Parkito's on the way</title>[m
[31m-[m
[31m-  <!-- Edit site and author settings in `_config.yml` to make the social details your own -->[m
[31m-[m
[31m-    <meta content="Parkito's on the way" property="og:site_name">[m
[31m-  [m
[31m-    <meta content="내가 생각하는 '좋은 코드'란 바로 이런 것이다" property="og:title">[m
[31m-  [m
[31m-  [m
[31m-    <meta content="article" property="og:type">[m
[31m-  [m
[31m-  [m
[31m-    <meta content="일개 개발자 지망생이 생각하는 '좋은 코드'란 무엇인지 일장 연설을 늘어놓겠습니다." property="og:description">[m
[31m-  [m
[31m-  [m
[31m-    <meta content="http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are" property="og:url">[m
[31m-	[m
[31m-  [m
[31m-    <meta content="2019-12-31T00:00:00+09:00" property="article:published_time">[m
[31m-    <meta content="http://localhost:4000/about/" property="article:author">[m
[31m-  [m
[31m-  [m
[31m-    <meta content="http://localhost:4000/assets/img/knowledge/literal-value-logo.jpg" property="og:image">[m
[31m-  [m
[31m-  [m
[31m-    [m
[31m-    <meta content="Programming" property="article:section">[m
[31m-    [m
[31m-  [m
[31m-  [m
[31m-    [m
[31m-    <meta content="good_code" property="article:tag">[m
[31m-    [m
[31m-    <meta content="clean_code" property="article:tag">[m
[31m-    [m
[31m-  [m
[31m-[m
[31m-    <meta name="twitter:card" content="summary">[m
[31m-    <meta name="twitter:site" content="@">[m
[31m-    <meta name="twitter:creator" content="@">[m
[31m-  [m
[31m-    <meta name="twitter:title" content="내가 생각하는 '좋은 코드'란 바로 이런 것이다">[m
[31m-  [m
[31m-  [m
[31m-    <meta name="twitter:url" content="http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are">[m
[31m-  [m
[31m-  [m
[31m-    <meta name="twitter:description" content="일개 개발자 지망생이 생각하는 '좋은 코드'란 무엇인지 일장 연설을 늘어놓겠습니다.">[m
[31m-  [m
[31m-  [m
[31m-    <meta name="twitter:image:src" content="http://localhost:4000/assets/img//knowledge/literal-value-logo.jpg">[m
[31m-  [m
[31m-[m
[31m-  [m
[31m-    <meta content="일개 개발자 지망생이 생각하는 '좋은 코드'란 무엇인지 일장 연설을 늘어놓겠습니다." name="description">[m
[31m-  [m
[31m-	<meta http-equiv="X-UA-Compatible" content="IE=edge">[m
[31m-	<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">[m
[31m-	<link rel="shortcut icon" href="/assets/img/favicon/favicon.ico" type="image/x-icon">[m
[31m-	<link rel="apple-touch-icon" href="/assets/img/favicon/apple-touch-icon.png">[m
[31m-	<link rel="apple-touch-icon" sizes="72x72" href="/assets/img/favicon/apple-touch-icon-72x72.png">[m
[31m-	<link rel="apple-touch-icon" sizes="144x144" href="/assets/img/favicon/apple-touch-icon-144x144.png">[m
[31m-	<!-- Chrome, Firefox OS and Opera -->[m
[31m-	<meta name="theme-color" content="#263959">[m
[31m-	<!-- Windows Phone -->[m
[31m-	<meta name="msapplication-navbutton-color" content="#263959">[m
[31m-	<!-- iOS Safari -->[m
[31m-	<meta name="apple-mobile-web-app-status-bar-style" content="#263959">[m
[31m-	<!-- Google Fonts -->[m
[31m-  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">[m
[31m-	<link href="https://fonts.googleapis.com/css?family=PT+Serif:400,700" rel="stylesheet">[m
[31m-	<link href="https://fonts.googleapis.com/css?family=Lato:300,400,700" rel="stylesheet">[m
[31m-[m
[31m-	<!-- Font Awesome -->[m
[31m-	<link rel="stylesheet" href="/assets/fonts/font-awesome/css/font-awesome.min.css">[m
[31m-	<!-- Styles -->[m
[31m-	<!-- Mathjax Support -->[m
[31m-<script type="text/javascript" async src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">[m
[31m-	MathJax.Hub.Config({[m
[31m-  showProcessingMessages: false,[m
[31m-  jax: ["input/TeX", "output/HTML-CSS"],[m
[31m-  TeX: {[m
[31m-    TagSide: "left",[m
[31m-    Macros: {[m
[31m-      RR: '{\\bf R}',[m
[31m-      bold: ['{\\bf #1}',1][m
[31m-    }[m
[31m-  },[m
[31m-  CommonHTML: {[m
[31m-    linebreaks: {automatic: true}[m
[31m-  }[m
[31m-});[m
[31m-</script>[m
[31m-[m
[31m-	<link rel="stylesheet" href="/assets/css/main.css">[m
[31m-	<link rel="stylesheet" href="/assets/css/personal.css">[m
[31m-	<link href="https://fonts.googleapis.com/css?family=Do+Hyeon|Nanum+Gothic:400,700,800&amp;subset=korean" rel="stylesheet">[m
[31m-[m
[31m-	<!-- googld ads tag -->[m
[31m-  <script data-ad-client="ca-pub-2670967175857332" async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>[m
[31m-</head>[m
[31m-[m
[31m-<body style="position: relative">[m
[31m-	<div id="toggler-wrapper">[m
[31m-		<div id="menu-toggler">[m
[31m-			<img src="/assets/img/nav-off.png" alt="Menu collapse image">[m
[31m-		</div>[m
[31m-	</div>[m
[31m-[m
[31m-  <div class="wrapper">[m
[31m-[m
[31m-		<nav id="nav">[m
[31m-			<div id="menus">[m
[31m-				<p>[m
[31m-					<a class="navbar-brand text-white" href="/">&nbsp;&nbsp;&nbsp;Parkito's on the way!&nbsp;&nbsp;&nbsp;</a>[m
[31m-				</p>[m
[31m-				<ul id="category-list">[m
[31m-					<li>[m
[31m-						<a href="/about.me">[m
[31m-							<div class="menu">[m
[31m-								<span> About </span>[m
[31m-							</div>[m
[31m-						</a>[m
[31m-					</li>[m
[31m-				[m
[31m-					<li>[m
[31m-						<div class="menu-wrapper">[m
[31m-							<a href="/category/programming">[m
[31m-								<div class="menu">[m
[31m-									<span> Programming </span>[m
[31m-								</div>[m
[31m-							</a>[m
[31m-							<div class="menu-item">[m
[31m-								<a href="/category/programming/knowledge">Knowledge</a>[m
[31m-								<a href="/category/programming/algorithm">Algorithm</a>[m
[31m-								<a href="/category/programming/python">Python</a>[m
[31m-								<a href="/category/programming/shell-programming">Shell programming</a>[m
[31m-							</div>[m
[31m-						</div>[m
[31m-					</li>[m
[31m-				[m
[31m-					<li>[m
[31m-						<div class="menu-wrapper">[m
[31m-								<a href="/category/insight">[m
[31m-									<div class="menu">[m
[31m-										<span> Insight </span>[m
[31m-									</div>[m
[31m-								</a>[m
[31m-								<div class="menu-item">[m
[31m-									<a href="/category/insight/sensitivity">&nbsp;&nbsp;Sensitivity&nbsp;&nbsp;</a>[m
[31m-									<a href="/category/insight/rationality">&nbsp;&nbsp;Rationality&nbsp;&nbsp;</a>[m
[31m-								</div>[m
[31m-						</div>[m
[31m-					</li>[m
[31m-[m
[31m-					<li>[m
[31m-						<div class="menu-wrapper">[m
[31m-								<a href="/category/projects">[m
[31m-									<div class="menu">[m
[31m-										<span> Projects </span>[m
[31m-									</div>[m
[31m-								</a>[m
[31m-							<div class="menu-item">[m
[31m-								<a href="/category/projects/dev-related">&nbsp;&nbsp;Dev related&nbsp;&nbsp;</a>[m
[31m-								<a href="/category/projects/etc">&nbsp;&nbsp;ETC&nbsp;&nbsp;</a>[m
[31m-							</div>[m
[31m-						</div> </li>[m
[31m-[m
[31m-				</ul>[m
[31m-			</div>[m
[31m-[m
[31m-			<div id="menus-right">[m
[31m-				<div id="search-section">[m
[31m-					<div class="input-wrapper">[m
[31m-						<span class="fa fa-search"></span>[m
[31m-						<input type="text" id="search-input" placeholder="Please input specific keyword :)" size="30">[m
[31m-					</div>[m
[31m-					<div id="results-container"></div>[m
[31m-				</div>[m
[31m-[m
[31m-				<!--<div id="toggler-wrapper">-->[m
[31m-					<!--<div id="menu-toggler">-->[m
[31m-						<!--<img src="/assets/img/nav-off.png" alt="" width="35px" height="35px">-->[m
[31m-					<!--</div>-->[m
[31m-				<!--</div>-->[m
[31m-				[m
[31m-			</div>[m
[31m-			[m
[31m-		</nav>[m
[31m-[m
[31m-[m
[31m-    <aside class="sidebar">[m
[31m-  <header>[m
[31m-    <div class="about">[m
[31m-      <div class="cover-author-image">[m
[31m-        <a href="/"><img src="/assets/img/1536558558520.jpg" alt="Sunghwan Park"></a>[m
[31m-      </div>[m
[31m-      <div class="author-name">Sunghwan Park</div>[m
[31m-      <p>I'm Parkito. A Python lover. Interested in Python, Automation, Algorithm. Please give me insights. I'll teach you tambien! :)</p>[m
[31m-    </div>[m
[31m-  </header> <!-- End Header -->[m
[31m-  <footer>[m
[31m-    <section class="contact">[m
[31m-      <h3 class="contact-title">Contact me</h3>[m
[31m-      <ul>[m
[31m-				<!--[m
[31m-        [m
[31m-          <li><a href="https://twitter.com/artemsheludko_" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a></li>[m
[31m-        [m
[31m-        [m
[31m-          <li><a href="https://facebook.com/" target="_blank"><i class="fa fa-facebook" aria-hidden="true"></i></a></li>[m
[31m-        [m
[31m-				-->[m
[31m-        [m
[31m-          <li class="github"><a href="http://github.com/shoark7" target="_blank"><i class="fa fa-github"></i></a></li>[m
[31m-        [m
[31m-        [m
[31m-          <li class="linkedin"><a href="https://in.linkedin.com/in/sunghwan-park-3773b8154" target="_blank"><i class="fa fa-linkedin"></i></a></li>[m
[31m-        [m
[31m-        [m
[31m-          <li class="email"><a href="mailto:shoark7@gmail.com"><i class="fa fa-envelope-o"></i></a></li>[m
[31m-        [m
[31m-      </ul>[m
[31m-    </section> <!-- End Section Contact -->[m
[31m-    <div class="copyright">[m
[31m-      <p>2020 &copy; Sunghwan Park</p>[m
[31m-    </div>[m
[31m-  </footer> <!-- End Footer -->[m
[31m-</aside> <!-- End Sidebar -->[m
[31m-[m
[31m-<div class="content-box clearfix">[m
[31m-  <article class="article-page">[m
[31m-  <div class="page-content">[m
[31m-    [m
[31m-    <div class="page-cover-image">[m
[31m-      <figure>[m
[31m-        <img class="page-image" src=/assets/img//knowledge/literal-value-logo.jpg alt="내가 생각하는 '좋은 코드'란 바로 이런 것이다">[m
[31m-        [m
[31m-      </figure>[m
[31m-    </div> <!-- End Page Cover Image -->[m
[31m-    [m
[31m-    <div class="wrap-content">[m
[31m-      <header class="header-page">[m
[31m-        <h1 class="page-title">내가 생각하는 '좋은 코드'란 바로 이런 것이다</h1>[m
[31m-        <div class="page-date"><span>2019, Dec 31&nbsp;&nbsp;&nbsp;&nbsp;</span></div>[m
[31m-      </header>[m
[31m-[m
[31m-		<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>[m
[31m-		<!-- 처음과끝에만 -->[m
[31m-		<ins class="adsbygoogle"[m
[31m-				 style="display:block"[m
[31m-				 data-ad-client="ca-pub-2670967175857332"[m
[31m-				 data-ad-slot="3352812061"[m
[31m-				 data-ad-format="auto"[m
[31m-				 data-full-width-responsive="true"></ins>[m
[31m-		<script>[m
[31m-				 (adsbygoogle = window.adsbygoogle || []).push({});[m
[31m-		</script>[m
[31m-		<!-- 처음과끝에만 -->[m
[31m-[m
[31m-      <h2 id="0-index">0. Index</h2>[m
[31m-[m
[31m-<blockquote>[m
[31m-  <ol>[m
[31m-    <li><a href="#1">들어가며</a></li>[m
[31m-    <li><a href="#2">좋은 코드란 그리 간단하지 않다</a></li>[m
[31m-    <li><a href="#3">성능</a>[m
[31m-      <ul>[m
[31m-        <li>3.1. <a href="#3a">개인적인 예들</a></li>[m
[31m-        <li>3.2. <a href="#3b">기타 성능이 중요할 수 있는 상황</a></li>[m
[31m-      </ul>[m
[31m-    </li>[m
[31m-    <li><a href="#4">재사용성</a>[m
[31m-      <ul>[m
[31m-        <li>4.1. <a href="#4a">모듈성</a></li>[m
[31m-        <li>4.2. <a href="#4b">범용성</a></li>[m
[31m-      </ul>[m
[31m-    </li>[m
[31m-    <li><a href="#5">구조화</a>[m
[31m-      <ul>[m
[31m-        <li>5.1. <a href="#5a">용어 정의: 구조화</a></li>[m
[31m-        <li>5.2. <a href="#5b">코드 단위의 구조화</a></li>[m
[31m-        <li>5.3. <a href="#5c">패키지 단위의 구조화</a></li>[m
[31m-      </ul>[m
[31m-    </li>[m
[31m-    <li><a href="#6">추상화</a>[m
[31m-      <ul>[m
[31m-        <li>6.1. <a href="#6a">용어 정의: 추상화</a></li>[m
[31m-        <li>6.2. <a href="#6b">코드 단의 추상화</a></li>[m
[31m-        <li>6.3. <a href="#6c">프로그램 단의 추상화</a></li>[m
[31m-      </ul>[m
[31m-    </li>[m
[31m-    <li><a href="#7">가독성</a>[m
[31m-      <ul>[m
[31m-        <li>7.1. <a href="#7a">변수 작명</a></li>[m
[31m-        <li>7.2. <a href="#7b">Coding convention</a></li>[m
[31m-        <li>7.3. <a href="#7c">사용자 고려</a></li>[m
[31m-        <li>7.4. <a href="#7d">기타: 주석과 여백</a></li>[m
[31m-      </ul>[m
[31m-    </li>[m
[31m-    <li><a href="#8">그래서 어쩌자고?</a></li>[m
[31m-    <li><a href="#9">마치며</a></li>[m
[31m-    <li><a href="#10">자료 출처</a></li>[m
[31m-  </ol>[m
[31m-</blockquote>[m
[31m-[m
[31m-<p><br id="1" /></p>[m
[31m-[m
[31m-<h2 id="1-들어가며">1. 들어가며</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p>나는 왜 블로그를 할까? 이 글을 쓸 생각을 하면서 문득 드는 생각이다. 처음엔 공부한 내용을 정리하고 또 다른 사람들과 공유하고 싶어서 시작했다. 그 순수한 마음에서 시작해 생각보다 블로그가 내 기준에서 사랑을 받으면서 왠지 더 많은 관심을 받을 주제들을 찾아 쓰게 됐다. 그렇다. 팔리는 글을 쓰기 시작한 것이다. 내가 특정 문제보다는 일반적인 주제의 포스트들을 찾아 쓰는 것은 일부분은 이런 이유도 있다.</p>[m
[31m-[m
[31m-<p>하지만 한편으로는 나 자신을 위해서 쓰는, 뭐랄까 도저히 안 쓰고는 못 배기겠는 주제들도 있다. 내가 정말 깊은 통찰을 느낀 인생의 경험들, 단순히 머리가 아닌 마음으로 이해하고 깨달아버린 지식들. 이런 주제들은 마음이 불러서 써야 한다. 보통 포스트를 너무 길게 쓰면 내용이 좋아도 외면 받는다. 하지만 이런 주제들은 외면 받을지라도 생각한 분량만큼 쓸 생각을 한다. 그래서 시간이 너무 소요되면 ‘이렇게까지 해야 하나’하는 생각이 들기도 한다.</p>[m
[31m-[m
[31m-<p>오늘 주제가 딱 그런 내용이다. 과연 <strong>‘좋은 코드’란 무엇일까?</strong> 개발자라면 한번은 고민해볼법한, 아니 사실 여러 번 고민했어야 할 주제. <strong>모든 상황에 적용되는 황금률 같은 정답은 없으나 상황에 맞는 정답을 만들어내는 주요 구성 요소들에 대한 내 고민의 결과들을 오늘 적어볼까 한다.</strong> 정말로, 도대체, 대관절 ‘좋은 코드’란 무엇인가?</p>[m
[31m-[m
[31m-<p><strong>나는 선배 개발자를 만났을 때, 또 면접 보러 가서 말미에 ‘당신이 생각하는 좋은 코드란 무엇이냐’는 질문을 반드시 던진다.</strong> 나보다 개발을 잘할테니 어떻게든 보고 배우기 위함이다. 지금까지 한 이십여명 물어본 것 같은데 참 반응들이 재밌다. 나름의 철학을 가진 사람도 있고, ‘읽기 좋은 코드’라고 무난하고 별 영양가 없는, 하지만 마냥 틀렸다고는 할 수 없는 정답을 말해주는 사람도 있고, 딱히 생각을 안 해봤는지 별다른 말을 못하거나 안하는 사람도 있다. 나의 이 글은 내 경험과 고민에서 비롯됐지만 이 분들의 영향도 결코 무시못한다. 그래서 이 글을 그분들께 바친다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>내용 구성은 먼저 <strong>‘좋은 코드 = 읽기 좋은 코드’가 아님을 살펴볼 것이다.</strong> 가독성은 좋은 코드의 매우매우 중요한 부분이지만 좋은 코드를 구성할 수 있는 요소는 이보다 더 많을 뿐더러 가독성이라는 말 자체도 너무 추상적이기 때문에 이런 까다로운 질문에 대한 쉽게 도망가는 대답밖에는 안 된다. 우리는 더 깊게 갈 것이다. 더 넓고 깊게.  <br />[m
[31m-<strong>그 다음 장부터는 내가 생각하는 좋은 코드의 주요 판단 요소들을 살펴볼 것이다. 이들은 성능, 재사용성, 구조화, 추상화, 가독성 등 5가지로 추렸고, 각 장마다 요소의 보다 구체적인 요소들을 실제 예시와 코드를 통해 살펴볼 것이다.</strong> 마지막으로는 이들을 고려해서 코드를 짜자는 개인적인 당부와 함께 글을 마치겠다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>들어가기 전 이것만큼은 이해해주길 바란다. 일단 코드는 전부 파이썬이고 난 현업 경험이 없어 예시로 드는 것들이 알고리즘이나 매우 간단한 코드일 수도 있다. 그리고 내용은 철저히 개인적인 주관에서 비롯되었고 비유나 설명을 위한 자료 조사는 하지만 이 로직과 구성은 이미 상당 부분 머릿속에 완성되어 있는 상태였다. 그래서 실력의 부족으로 누락된 중요한 요소, 논리의 모순, 내용의 어설픔 등이 있을 수 있는데 이는 댓글로 지적해주시면 깊이 고민해보겠다. 솔직히 말하면 내용이 어설플 것 같아서 벌써부터 자괴감이 들기는 한다.</p>[m
[31m-[m
[31m-<p>어쩌다보니 크리스마스 특집으로 쓰게 됐네. 그 전에는 써야겠지? 그래야 최근에 나온 영화 ‘아이리시맨’을 그날 볼 수 있을테니까.</p>[m
[31m-[m
[31m-<p>시작합니다.</p>[m
[31m-[m
[31m-<p><br />[m
[31m-<br id="2" /></p>[m
[31m-[m
[31m-<h2 id="2-좋은-코드란-그리-간단한-문제가-아니다">2. 좋은 코드란 그리 간단한 문제가 아니다</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p>내가 선배 개발자들에게 ‘좋은 코드가 뭐라고 생각하세요?’라고 물어보면 십중팔구 <strong>코드의 가독성</strong>을 이야기한다. 거의 대부분이 가독성을 언급하는데 물론 좋은 대답이다. 우리는 본인이 폰 노이만이나 리누스 토발즈가 아닌 이상 회사에서 협업을 하게 될 것이고 거대한 시스템이나 기능의 일부를 함께 개발하기에 서로가 서로의 코드를 이해할 수 있어야 한다. 이런 이슈를 많이 겪을 현업인들에게 물어서 그런지 답변의 95% 이상이 가독성을 이야기하는 것은 이상하지 않고 <strong>나도 가독성이 좋은 코드의  매우, 또는 가장 중요한 요소라고 생각한다.</strong></p>[m
[31m-[m
[31m-<p>하지만 첫 장에서 언급했듯이 <strong>좋은 코드의 조건을 ‘가독성’에 한해서 이야기하는 것은 부적절하다.</strong> 일단 내가 질문했을 때 5%의 사람들은 가독성 이외의 대답을 줬다. 가독성도 중요하겠지만 지금 자신들의 상황에서는 다른 요소가 더 중요하다는 것을 뜻한다.</p>[m
[31m-[m
[31m-<p>또한 <strong><code class="highlighter-rouge">가독성</code> 용어 자체가 너무 모호하며 기업 크기, 현재 개발 상황, 사업하는 도메인, 리드 개발자 성향 등에 따라 천차만별일 수 있다.</strong> 이는 ‘정의’, ‘진리’ 등이 무엇이냐고 묻는 것과 비슷한 것으로 모두가 만족할 수 있는 정답같은 것은 없다.<br />[m
[31m-매우 간단한 예를 들어보자면 어떤 사람들은 주석이 없어도 잘 읽히는 코드가 중요하다고 생각한다. 이런 사람들은 주석을 최대한 피하는 것을 지향한다. 하지만 어떤 사람들의 말을 들어보면 적재적소의 주석을 매우 긍정적으로 생각하기도 한다. 좋은 코드에 대한 이런 이슈 등은 정말 오랜 토론의 대상이 되어 왔고, 개인적인 생각에 이는 정말 스타일의 차이로 밑의 가독성 장에서도 언급할 예정이다.</p>[m
[31m-[m
[31m-<p><img src="/assets/img/knowledge/good_codes_moon.png" alt="달의 위상 변화" /></p>[m
[31m-[m
[31m-<p>이 장을 쓰면서 <code class="highlighter-rouge">좋은 코드</code>에 대한 좋은 비유가 떠올랐다. <strong>좋은 코드를 달에 비유할 수 있겠다.</strong> 달은 다 알다시피 지구의 하나뿐인 위성으로 기상이 좋으면 거의 매일 볼 수 있는데 자체 발광하지 않고 태양의 빛을 반사해서 우리가 지구에서 볼 수 있다. 그래서 지구와 달, 태양의 위치에 따라 지구에서 보이는 달의 모습이 조금씩 달라진다. 그 모습을 위상(phase)이라고 하며 위 사진은 지구와 달, 태양의 위치에 따른 달의 위상 변화에 대한 이미지로 이 위상들은 우리에게 익숙한 보름달, 초생달, 그믐달 등의 용어로 표현되고는 한다.</p>[m
[31m-[m
[31m-<p>여기에 더해 다는 모르는 내용으로는 달은 지구를 중심으로 도는 공전주기와 자체 회전하는 자전주기가 같아 지구에서는 달의 한 쪽면만을 볼 수 있다. 다른 말로 하면 <strong>우리가 지구에서 사는 이상 달의 뒷면은 결코 볼 수 없다는 것이다.</strong></p>[m
[31m-[m
[31m-<p><strong>좋은 코드는 달과 같다.</strong> 우리는 새벽녘에 특유의 감성을 불어넣는 달을 사랑하며 좋은 코드인 달에 대해 모든 것을 알고 싶어하고, 또 알고 있다고 자부한다. 지구에서 달을 바라보며, 달이 명확히 시야에 보이기 때문에 ‘좋은 코드란 저런 것이다’라고 단정짓는 것이다. 이때 <strong>우리가 볼 수 있는 달의 모습, 위상은 가독성을 상징한다. 가독성은 좋은 코드의 가장 중요하고 명확한 요소 중 하나이기 때문이다.</strong></p>[m
[31m-[m
[31m-<p>하지만 우리가 의식적으로 노력하지 않는 이상, <strong>우리는 달의 온전한 모습을 보지 못한다. 과학이 발달하고 천문학자들의 노력이 있었기에 우리는 우리가 보는 달의 모습이 달의 전부가 아님을 안다. 위상이 곧 본체가 아니듯, 가독성이 곧 좋은 코드의 유일한 조건은 아닌 것이다.</strong> 과연 달의 뒷면은 어떻게 생겼을까? 앞면과는 다른 특징이 있을까? 우리는 더 노력해야 한다. 좋은 코드의 다른 조건들도 더 탐구해봐야 하는 것이다.</p>[m
[31m-[m
[31m-<p>또한 우리가 보는 달의 모습 또한 시시각각 변한다. 이는 우리에게 너무 익숙하며 음력 달력은 이런 달의 위상을 기준으로 한다. 가독성의 모습 또한 상황에 따라 변할 수 있는 것. 이렇기에 지금 이 시점에 달을 손가락으로 가리키며 ‘달이란 과연 저런 것이다’라고 말하는 것은 어불성설이라 하겠다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>우리는 달에 대한 우리의 이해가 부족함을 깨달았고 이제 달의 뒷면을 조사할 것이다. 달의 뒷면은 무엇들로 구성되어 있는가? 그리고 지구에서 볼 수 있는 각 위상들도 마찬가지로 탐구 대상이다. 달은 반지름이 약 1700km에 달하는 매우 큰 천체로 쉽지만은 않을 것이다. 하지만 포기할 수 없다. 다음 장부터 본격적으로 살펴보도록 하자.</p>[m
[31m-[m
[31m-<p><br />[m
[31m-<br id="3" /></p>[m
[31m-[m
[31m-<h2 id="3-성능">3. 성능</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p>내가 아는 한 컴공을 전공하는 모든 학생들은 <code class="highlighter-rouge">알고리즘</code> 수업을 듣는다. 알고리즘은 현실의 다양한 문제를 컴퓨터를 통해 해결하는 방법을 배우는데 이중 꼭 배우는 개념으로 <code class="highlighter-rouge">시공간 복잡도(time and space complexity)</code>가 있다. <strong>복잡도는 문제를 해결하는 방법의 성능을 논하는 개념으로 단순히 문제를 해결하는 것뿐만 아니라 얼마나 효율적으로 이 문제를 해결하는지도 중요하다는 것을 의미한다.</strong> 이중 성능의 표기법으로 모두가 아는 <script type="math/tex">Big O Notation</script>이 유명하며, 학교에서가 아니더라도 알고리즘을 조금만 배우면 이 성능 표기법은 다 배우기 마련이다. <strong>성능의 두 척도는 시간과 공간으로</strong> 시간은 이 알고리즘이 문제를 해결하는 데 대략 얼마나 시간이 소요되는지, 공간은 해결하는 데 메모리가 얼마나 소요될지를 논한다. 또한 현대 전산 과학에서는 공간 복잡도보다는 시간복잡도를 더 많이 이야기한다.</p>[m
[31m-[m
[31m-<p><strong>나같은 사람은 실제 대량의 트래픽을 다룬다는가 하는 현업 프로젝트 경험이 없고, 대신 알고리즘 문제만 주구장창 많이 풀었다보니 한때 성능이 좋은 코드의 가장 중요한 척도라고 생각했다.</strong> 알고리즘 문제 연습 플랫폼들에서 비효율적인 알고리즘을 효율적인 알고리즘으로 바꾸어 문제를 통과하는 것을 보며 그 신화를 내적으로 강화했고 그외에는 생각하지 않았다.</p>[m
[31m-[m
[31m-<p>그러던 중 Alan이라는 사람을 만나 <strong>좋은 코드의 다른 가능성을 알게 되었다.</strong> 매우 기초적으로 ‘매직 스트링, 넘버를 피한다든가’, ‘필요하다면 변수, 상수를 구분하라’와 같은 것들로서 아래 가독성 파트에서 다룰 것이다. 짧은 순간이었지만 그 가르침은 내 코드 인생을 바꿨으며 모듈화, 구조화 등에 대한 관심까지 이어진다. 그 형이 아니었으면 이 포스트는 만들어지지 않았을 수도 있다. 그 형께 이 자리를 빌어 진심으로 감사를 전한다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p><strong>난 올해 처음 취업 시장에 조금씩 뛰어들면서 선배 개발자들에게 그 질문을 던졌을 때 <code class="highlighter-rouge">성능</code>을 언급하는 사람들이 거의 전무하다는 것에 놀랐다.</strong> 솔직히 한 절반 정도는 성능을 이야기할 줄 알았다. 하지만 대부분이 가독성을 언급했고 그래서 검색창에 좋은 코드라고 검색했을 때 ‘성능’을 언급하는 포스트를 찾기 힘들다는 것이 전혀 놀랍지 않다.</p>[m
[31m-[m
[31m-<p>하지만 분명히 말하지만 <strong>성능은 좋은 코드의 조건이 될 수 있다.</strong> 아무리 하드웨어의 발달로 전산능력이 향상되고 메모리 용량이 커진다고 해서 성능 문제가 만사해결되는 것은 아니다. 시간과 공간 성능 중요도에 대해 개인적인 예들과 합리적인 코드 예로 살펴볼 것이다.</p>[m
[31m-[m
[31m-<p><br id="3a" /></p>[m
[31m-[m
[31m-<h3 id="31-개인적인-예들">3.1. 개인적인 예들</h3>[m
[31m-[m
[31m-<p>첫 번째 예는 알고리즘 주식 거래 회사에 면접 보면서 깨닫게 됐다. 면접을 보고 말미에 면접관들에게 ‘좋은 코드가 뭐라고 생각하세요?’라는 익숙한 질문을 던졌다. 그중 한 분이 ‘좋은 코드는 상황에 따라 너무 달라서 뭐라 하기가 힘든데… 일단 저희는 <strong>실시간으로 가격 등락에 따라 거래가 바로바로 이루어져야 하기 때문에 latency(요청과 응답 사이의 시간 지연)가 낮은 코드가 중요한 것 같아요.’</strong></p>[m
[31m-[m
[31m-<p>이분이 성능이 중요하다고 말한 첫 분이었다. 그때 난 느꼈다. <strong>이 회사는 물론 가독성 많은 요소가 정말정말 중요하겠지만 이 회사의 특수성상 시간 성능이 Mission critical하다.</strong> 애초에 시간 성능이 충족되지 않으면 사업이 지속가능하지 않은 것이다. 아마 이 회사의 경우 코드의 가독성이 떨어진다고 해서 사업이 망하지는 않을 것이다. 그래서 가독성보다 성능이 더 중요한 예라고 하겠다.</p>[m
[31m-[m
[31m-<p>조금 다른 얘기로 난 면접이 끝나고 이 대답을 곰곰히 생각하면서 내가 수집하는 데이터가 조금 편향되었을 수 있겠다고 생각했다. 내가 면접을 본 곳들은 보통 실시간 어플리케이션을 다루는 곳이 아닌, 일반적인 기대 시간 안에 요청을 수행하면 되는 어플리케이션을 개발하는 곳들이었다. ‘특별한 철학이 있는 곳이 아닌 이상 이런 곳들이 좋은 코드에 대해 할 수 있는 말이 가독성 이외에 특별히 있을까?’하는 생각이 들기는 했다. 무시하는 것이 아니고 의도치 않게 요구사항이 무난한 곳에서만 면접을 보게 돼서 대답들이 편향되었을 수 있지 않을까 하는 것이다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>다른 예로는 파이콘에서 들은 이야기가 있다. 파이콘에서는 항상 라이트닝 토크라고 하여 현장에서 신청한 사람들에게 주제 상관없이 5분 간 발표를 할 수 있는 기회를 준다. 몇 년 전인지는 기억이 안 나지만 그때 라이트닝 토크에서 임베디드 프로그래밍을 하는 사람이 발표를 하면서 <strong>자신이 개발하는 기기에는 일반 컴퓨터와 달리 메모리가 극히 제한적이기 때문에 코딩할 때 그 부분을 중점으로 둔다고 했다.</strong> 이 또한 성능이 극히 중요할 수 있는 예라고 하겠다. 위의 예가 시간 성능이었다면 이 예는 공간 성능이 중요한 상황.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>위와 같은 예가 결코 개발하는 상황의 절대다수라고 말할 수는 없을 것이다. 하지만 위와 같은 상황이 얼마든지 존재하고 따라서 가독성을 좋은 코드의 절대 조건이라고 말하는 것은 힘들어 보인다.</p>[m
[31m-[m
[31m-<p><br id="3b" /></p>[m
[31m-[m
[31m-<h3 id="32-기타-성능이-중요할-수-있는-상황">3.2. 기타 성능이 중요할 수 있는 상황</h3>[m
[31m-[m
[31m-<p>성능 관련 장을 기획하면서 괜찮겠다고 생각한 몇몇 상황이 있다. 위의 예시가 내가 직접 경험한 것이라면 이 절의 두 예는 알고리즘 적으로 일리가 있다고 생각하는 것들을 가져왔다.</p>[m
[31m-[m
[31m-<p>먼저 순차탐색과 이진탐색. 이진탐색은 알고리즘을 조금 공부해보면 고생하게 되는 주제로 정렬된 1차원 배열에서 특정값이 어느 인덱스에 위치하고 있는지를 찾는 알고리즘을 말한다. 다 알다시피 이진(binary)라는 이름이 붙은 것은 원하는 값이 나올 때까지 배열을 절반으로 가르면서 탐색을 진행하기 때문이다. 따라서 이진탐색의 시간복잡도는 <script type="math/tex">O(logN)</script>이 된다. 반대로 순차탐색은 배열을 말 그대로 순서대로 훑으면서 값을 찾는데, 한 번 탐색할 때마다 탐색할 배열의 크기가 절반이 아닌 1이 줄어들기 때문에 시간복잡도는 <script type="math/tex">O(N)</script>이 된다. 시간복잡도상 이진탐색이 순차탐색에 비해 절대 우위에 있다.</p>[m
[31m-[m
[31m-<p>하지만 성능이 아닌 이슈로 넘어가보면 어떨까? 정렬된 배열 <em>arr</em> 에 대해 특정값 <em>v</em> 를 찾는 순차탐색, 이진탐색의 코드는 각각 다음과 같다.</p>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1"># 순차탐색[m
[31m-</span><span class="k">def</span> <span class="nf">sequential_search</span><span class="p">(</span><span class="n">arr</span><span class="p">,</span> <span class="n">v</span><span class="p">):</span>[m
[31m-    <span class="k">for</span> <span class="n">i</span><span class="p">,</span> <span class="n">n</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">arr</span><span class="p">):</span>[m
[31m-        <span class="k">if</span> <span class="n">n</span> <span class="o">==</span> <span class="n">v</span><span class="p">:</span>[m
[31m-            <span class="k">return</span> <span class="n">i</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1"># 재귀함수를 사용한 이진탐색[m
[31m-</span><span class="k">def</span> <span class="nf">binary_search</span><span class="p">(</span><span class="n">arr</span><span class="p">,</span> <span class="n">v</span><span class="p">):</span>[m
[31m-    <span class="k">def</span> <span class="nf">search</span><span class="p">(</span><span class="n">lo</span><span class="p">,</span> <span class="n">hi</span><span class="p">):</span>[m
[31m-        <span class="k">if</span> <span class="n">lo</span> <span class="o">==</span> <span class="n">hi</span><span class="p">:</span>[m
[31m-            <span class="k">return</span> <span class="n">lo</span>[m
[31m-        <span class="n">mid</span> <span class="o">=</span> <span class="p">(</span><span class="n">lo</span> <span class="o">+</span> <span class="n">hi</span><span class="p">)</span> <span class="o">//</span> <span class="mi">2</span>[m
[31m-        <span class="k">if</span> <span class="n">arr</span><span class="p">[</span><span class="n">mid</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="n">v</span><span class="p">:</span>[m
[31m-            <span class="k">return</span> <span class="n">search</span><span class="p">(</span><span class="n">lo</span><span class="p">,</span> <span class="n">mid</span><span class="p">)</span>[m
[31m-        <span class="k">else</span><span class="p">:</span>[m
[31m-            <span class="k">return</span> <span class="n">search</span><span class="p">(</span><span class="n">mid</span><span class="o">+</span><span class="mi">1</span><span class="p">,</span> <span class="n">hi</span><span class="p">)</span>[m
[31m-[m
[31m-    <span class="k">return</span> <span class="n">search</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">arr</span><span class="p">))</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<p>각 탐색을 무난하게 구현했다. 이때 성능이 아닌 가독성의 측면에서 보자. 그러면 <strong>순차탐색이 이진탐색에 비해 압도적으로 가독성이 좋은 것을 알 수 있다.</strong> 애초에 순차탐색은 프로그래밍을 처음 배우는 사람도 반복문과 조건문만 배우면 짜볼 수 있는데 반해 이진탐색은 알고리즘을 조금 공부해본 사람도 버그 없는 코드를 짜기 어렵다. 실제로 버그 없는 이진탐색 코드는 1962년에야 작성되었으며 이진탐색은 취업면접에서도 낼 수 있는 수준의, 마냥 쉽지 않은 알고리즘이다.</p>[m
[31m-[m
[31m-<p><strong>그럼에도 위와 같은 문제상황이라면 백이면 백 이진탐색 알고리즘을 쓸 것이다.</strong> 가독성이 순차탐색에 비해 안 좋지만 성능이 압도적으로 좋기 때문이다. 특히 배열의 크기가 크다고 해보자. 가령 배열의 크기가 10억 정도 된다고 할 때 순차탐색은 최대 10억번의 탐색을 해야하지만 이진탐색은 30번 정도(<script type="math/tex">log_210^9</script>)면 된다. 30과 10억은 정말 말도 안 되는 차이기 때문에 이 정도 크기가 되면 누구나 이진탐색을 쓰지 않을까? 코드가 어렵다고 탓할 것이 아니라 이쯤되면 ‘내가 어떻게든 이해해볼게’가 될 것이다. 즉 <strong>가독성을 성능이 찍어누를 수도 있다는 것.</strong></p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>다음 경우는 페이스북을 보면서 생각이 들었다. 페이스북은 유저와 유저가 친구를 맺을 수 있으며 이런 소셜 네트워크는 그래프 자료구조로 표현하기 딱 알맞은 자료구조다. 각 유저를 노드 또는 정점(vertex)로 두고 친구 관계가 링크 또는 엣지(edge)가 되는 것이다. 이때 모든 유저의 집합을 V, 모든 친구관계의 집합을 E라고 하자. 그래프 자료구조를 구현하는 방법은 크게 두 가지인데, 하나는 <code class="highlighter-rouge">|V|</code>개의 인접 배열을 사용하는 방법과 <code class="highlighter-rouge">|V|</code>개의 인접 리스트를 사용하는 것이다.(<code class="highlighter-rouge">| |</code>는 안의 집합의 크기를 구하는 연산자로 간주하자) 각각의 구현은 서로를 보완하는 장단점을 갖는데 여기서는 공간만 이야기해보자. <strong>인접 리스트를 사용하는 방법은 <script type="math/tex">O(\|V\|+\|E\|)</script>의 공간복잡도가 소요되고 인접 행렬은 <script type="math/tex">(\|V\|^2)</script>만큼의 공간복잡도가 소요된다.</strong> 이 내용들은 그래프를 처음 배울 때 기본으로 익히고 시작하는 것들이다. <strong>우리가 이 친구 관계를 그래프로 표현해야 할 때, 어떤 구현방법을 선택할지는 유저 집합 V와 친구 관계 집합 E의 크기에 따라 고려할 수도 있을 것이다.</strong></p>[m
[31m-[m
[31m-<p>공간만 고려했을 때는 일반적으로 두 구현 중 E가 V에 비해 지나치게 작은 희소 그래프(sparse graph)일 때는 인접 리스트를 사용하고, 관계가 충분히 많은 밀집 그래프(dense graph)일 때는 인접 행렬을 사용하는 것이 유리하다. 그 이유는 공간복잡도만 봐도 알 수 있는데 그래프가 희소하다는 말은 E의 크기가 작다는 뜻으로 이때 사용되는 공간은 <script type="math/tex">O(\|V\|+\|E\|)</script>로 그 반대에 비해 사용 공간이 훨씬 절약될 수 있기 때문이다. 반면 E의 크기가 V의 크기에 비해 그리 작지 않거나 더 많을 수 있는 밀집 그래프의 경우에는 공간복잡도상 그리 차이가 나지 않으면서 추가적으로 특정 연산에서의 시간성능 향상을 기대할 수 있다.</p>[m
[31m-[m
[31m-<p>자, 그럼 우리가 페이스북 CTO라고 해보자. 친구 관계는 페이스북의 핵심 기능이기 때문에 이 친구 관계를 그래프 자료구조로 표현하는 일이 매우 중요하다. 여기서는 follow 등은 신경쓰지 말고 오로지 친구를 맺는 기능만 생각한다. <strong>문득 생각할 때 두 그래프 구현 중 어떤 구현이 페이스북의 친구 그래프를 표현하기에 적합할까?</strong></p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>작년 자료를 보니 페이스북의 월간 활성 사용자수는 22억명이라고 한다. 편의를 위해 20억명이라고 하자. 물론 활성 사용자가 총 계정수는 아니지만 정확한 계정수를 파악할 수 없었기 때문에 약 20억개 이상의 계정이 존재하고 편의상 20억이라고 잡자. 이때 이 20억명의 집합이 V가 되며 |V|가 20억이 된다. 다음은 E를 추정해보자. 당신에게 묻는다. 당신이 페이스북 계정이 있다면, 등록된 친구수는 몇 명인가? 통계 자료에 의하면 페이스북 유저들의 평균 친구수는 338명이라고 한다. 중위수는 200명으로 이는 소수의 유저들이 친구수가 매우 많다는 것을 뜻한다.(한마디로 소수의 인싸들이 평균을 확 높이고 있다는 얘기)</p>[m
[31m-[m
[31m-<p><strong>중요한 것은 등록된 유저수에 비해 개인의 평균 친구수는 너무 적어서 이 그래프는 어떻게 표현해도 희소 그래프라는 것이다.</strong> 인접 행렬 구현은 공간복잡도가 <script type="math/tex">O(\|V\|^2)</script>로 대략 <script type="math/tex">4 * 10^{16}</script> 정도의 공간을 잡아야 한다. 반대로 인접 리스트 구현은 한 유저당 |V|만큼이 아닌, 평균적으로 338개의 공간이 필요하니 <script type="math/tex">E</script>의 크기가 대략 20억 * 338(<script type="math/tex">6 * 10^{10}</script>)가 된다. 이때 공간복잡도는 <script type="math/tex">O(\|V\| + \|E\|)</script>로 1천억(<script type="math/tex">10^{11}</script>)을 넘지 않기 때문에 이 경우에는 인접 리스트 구현이 더 유리한 것이 된다. <strong>무엇보다 두 구현의 공간복잡도 차이가 너무 압도적이기 때문에 내 생각에 이 결정에 있어 성능을 결코 무시할 수 없는 것이다.</strong> 따라서 이또한 성능이 좋은 코드의 중요한 요소가 될 수 있는 예라고 하겠다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>이처럼 내가 들은 실제 예와 충분히 고민 가능한 시나리오를 훑어보면서 <strong>우리는 때로는 성능이 코드 결정에 중요한 역할을 할 수 있다는 것을 알게 됐다.</strong> 면접을 보러 가서 ‘좋은 코드는 성능 좋은 코드입니다!’라고 말하는 것은 위험할 수 있지만 ‘좋은 코드의 조건 중에는 성능도 있다고 생각합니다’는 충분히 괜찮은 의견이 될 수 있을 것이다.</p>[m
[31m-[m
[31m-<p>이번 장이 좀 길어졌는데 다음 장부터 가독성 이전까지는 이보다 짧아지리라 기대한다.</p>[m
[31m-[m
[31m-<p><br />[m
[31m-<br id="4" /></p>[m
[31m-[m
[31m-<h2 id="4-재사용성">4. 재사용성</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p>이 주제는 알고리즘으로 개발을 주로 하는 사람들, 나같은 사람들에게는 가장 낯선 주제다. 재사용성(reusability)이라. 재사용성은 당연하게도 한 번 작성했어도 다음 기회에 다시 사용할 수 있는 코드의 특징을 말한다. <strong>재사용성이 낮은 코드는 특정 문제에만 지나치게 특화되어 비슷한 상황에서도 다시 쓸 수 없는 코드를 말하고 재사용성이 높으면 구체적인 값과 syntax는 달라도 비슷한 유형의 문제상황이라면 이 코드를 조금만 수정해 다시 사용할 수 있게 된다.</strong> 이런 예를 곧 보게 될 것이다.</p>[m
[31m-[m
[31m-<p>알고리즘 문제를 푸는 사람들은 이런 재사용성을 전혀 신경쓰지 않고 코드를 짠다. 물론 그것이 이해는 간다. 당장 이 문제를 통과하면 이 문제를 당장 다시 보는 일은 없을 것이기 때문이다. 하지만 난 의아하게 생각한다. <strong>현업에서 코드를 작성하고 다시 사용하는 일은 결코 없는 일일까?</strong> 적어도 내가 들은 바에 의하면 그렇지 않다. SI 업체 같은 곳에서 선배가 짜놓은 코드를 세부사항만 수정하고 다시 쓰는 일이 꽤 있고, 프로그래밍이 아닌 재무쪽이지만 선배가 짜놓은 엑셀 파일을 매일 업무에 활용하는 경우도 들을 수 있었다.</p>[m
[31m-[m
[31m-<p>느낀 바는 <strong>재사용성 높은 코드를 적절히 활용하면 실제 창의적인 업무와 관련 없는 지루한 작업을 매번 재계산할 필요없이 시간을 절약하고 코드를 짤 수 있겠다고 생각했다.</strong> 그리고 <strong>재사용성 높은 코드의 중요한 특징을 두 가지 추렸는데 크게 모듈성과 범용성이 있겠다.</strong></p>[m
[31m-[m
[31m-<p><br id="4a" /></p>[m
[31m-[m
[31m-<h3 id="41-모듈성">4.1. 모듈성</h3>[m
[31m-[m
[31m-<p><strong>모듈성(modularity)은 파이썬의 모듈(module)에만 국한되지 않는 소프트웨어 공학적인 용어로서 하나의 기능 단위가 하나의 작업만 하는 것을 뜻한다.</strong> 이는 리눅스 쉘 명렁어 프로그램들의 주요한 특징으로 리눅스 CLI에서는 복잡한 기능을 하는 하나의 함수가 아니라 여러 개의 단순한 기능을 하는 기능들을 파이프라이닝(pipelining) 등을 통해 조합해 더 큰 일을 하는 것을 지향한다.</p>[m
[31m-[m
[31m-<p>이렇게 하나의 프로그램을 보다 단순하게 만드는 모듈성이 지니는 가치는 재사용성과 직결된다. 생각해보자. 여러 작업을 동시에 하는, 복잡한 기능을 한 번에 처리하는 기능에 대한 요구사항이 정말 그렇게 많을까? 상식적으로 생각해도 처리하는 기능이 많으면 많을수록 점점 그 기능은 보다 특수한 상황에 적합한 용도의 프로그램이 되고 덜 일반적인 프로그램이 된다. 하지만 단순한 기능의 프로그램을 여러 개 만들고 그들을 조합해 큰 기능을 하게 만든다면 각각의 단순한 기능은 각각이 필요한 상황이 독립적으로 여럿 생길 수 있다. 즉 전체 재사용성이 증대되는 것이다.</p>[m
[31m-[m
[31m-<p>모듈성을 고려할만한 예제를 하나 준비했다. 최근에 푼 <a href="https://algospot.com/judge/problem/read/CHRISTMAS">알고리즘 문제</a>로 두 가지 형태의 코드를 제시한다. <strong>이 문제는 한 문제에서 두 가지의 부분문제를 동시에 풀 것을 요구했는데 두 부분문제를 한 기능 내에서 해결할 수도 있고, 각 부분문제를 독립적인 모듈로 만들어 이들을 조합해 전체 문제를 풀 수도 있겠다.</strong> 순서대로 코드를 보자. 두 코드 다 정답을 반환하기는 한다.</p>[m
[31m-[m
[31m-<p>모듈성 낮은 코드:</p>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="kn">from</span> <span class="nn">collections</span> <span class="kn">import</span> <span class="n">Counter</span>[m
[31m-[m
[31m-<span class="n">MOD</span> <span class="o">=</span> <span class="mi">20091101</span>[m
[31m-[m
[31m-[m
[31m-<span class="k">def</span> <span class="nf">solve_two_problems</span><span class="p">(</span><span class="n">doll_boxes</span><span class="p">,</span> <span class="n">K</span><span class="p">):</span>[m
[31m-    <span class="n">cumul_dolls</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span><span class="p">]</span>[m
[31m-    <span class="k">for</span> <span class="n">doll</span> <span class="ow">in</span> <span class="n">doll_boxes</span><span class="p">:</span>[m
[31m-        <span class="n">cumul_dolls</span><span class="o">.</span><span class="n">append</span><span class="p">((</span><span class="n">cumul_dolls</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">+</span> <span class="n">doll</span><span class="p">)</span> <span class="o">%</span> <span class="n">K</span><span class="p">)</span>[m
[31m-[m
[31m-    <span class="c1"># 1. Count total number of ways to buy dolls[m
[31m-</span>    <span class="n">counter</span> <span class="o">=</span> <span class="n">Counter</span><span class="p">(</span><span class="n">cumul_dolls</span><span class="p">)</span>[m
[31m-    <span class="n">total_ways</span> <span class="o">=</span> <span class="mi">0</span>[m
[31m-[m
[31m-    <span class="k">for</span> <span class="n">way</span> <span class="ow">in</span> <span class="n">counter</span><span class="o">.</span><span class="n">values</span><span class="p">():</span>[m
[31m-        <span class="k">if</span> <span class="n">way</span> <span class="o">&gt;=</span> <span class="mi">2</span><span class="p">:</span>[m
[31m-            <span class="n">total_ways</span> <span class="o">+=</span> <span class="n">way</span> <span class="o">*</span> <span class="p">(</span><span class="n">way</span> <span class="o">-</span> <span class="mi">1</span><span class="p">)</span> <span class="o">//</span> <span class="mi">2</span>[m
[31m-[m
[31m-    <span class="n">total_ways</span> <span class="o">%=</span> <span class="n">MOD</span>[m
[31m-[m
[31m-[m
[31m-    <span class="c1"># 2. Maximum number of consecutive buys[m
[31m-</span>    <span class="n">ret</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span><span class="p">]</span> <span class="o">*</span> <span class="nb">len</span><span class="p">(</span><span class="n">cumul_dolls</span><span class="p">)</span>[m
[31m-    <span class="n">prev</span> <span class="o">=</span> <span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span> <span class="o">*</span> <span class="n">K</span>[m
[31m-[m
[31m-    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">cumul_dolls</span><span class="p">)):</span>[m
[31m-        <span class="k">if</span> <span class="n">i</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>[m
[31m-        <span class="k">else</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>[m
[31m-[m
[31m-        <span class="n">loc</span> <span class="o">=</span> <span class="n">prev</span><span class="p">[</span><span class="n">cumul_dolls</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span>[m
[31m-        <span class="k">if</span> <span class="n">loc</span> <span class="o">!=</span> <span class="o">-</span><span class="mi">1</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">ret</span><span class="p">[</span><span class="n">loc</span><span class="p">]</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span>[m
[31m-[m
[31m-        <span class="n">prev</span><span class="p">[</span><span class="n">cumul_dolls</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">=</span> <span class="n">i</span>[m
[31m-[m
[31m-    <span class="n">max_buys</span> <span class="o">=</span> <span class="n">ret</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>[m
[31m-[m
[31m-    <span class="k">return</span> <span class="n">total_ways</span><span class="p">,</span> <span class="n">max_buys</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<p>모듈성 높은 코드:</p>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">def</span> <span class="nf">ways_buying</span><span class="p">(</span><span class="n">p_gifts</span><span class="p">,</span> <span class="n">K</span><span class="p">):</span>[m
[31m-    <span class="n">MOD</span> <span class="o">=</span> <span class="mi">20091101</span>[m
[31m-    <span class="n">counter</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">K</span><span class="p">)]</span>[m
[31m-    <span class="n">ret</span> <span class="o">=</span> <span class="mi">0</span>[m
[31m-[m
[31m-    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">p_gifts</span><span class="p">)):</span>[m
[31m-        <span class="n">counter</span><span class="p">[</span><span class="n">p_gifts</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">+=</span> <span class="mi">1</span>[m
[31m-[m
[31m-    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">K</span><span class="p">):</span>[m
[31m-        <span class="k">if</span> <span class="n">counter</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">&gt;=</span> <span class="mi">2</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span> <span class="o">=</span> <span class="p">(</span><span class="n">ret</span> <span class="o">+</span> <span class="p">((</span><span class="n">counter</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">*</span> <span class="p">(</span><span class="n">counter</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">-</span> <span class="mi">1</span><span class="p">))</span> <span class="o">//</span> <span class="mi">2</span><span class="p">))</span> <span class="o">%</span> <span class="n">MOD</span>[m
[31m-    <span class="k">return</span> <span class="n">ret</span>[m
[31m-[m
[31m-[m
[31m-<span class="k">def</span> <span class="nf">max_buys</span><span class="p">(</span><span class="n">p_gifts</span><span class="p">,</span> <span class="n">K</span><span class="p">):</span>[m
[31m-    <span class="n">ret</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">p_gifts</span><span class="p">))]</span>[m
[31m-    <span class="n">prev</span> <span class="o">=</span> <span class="p">[</span><span class="o">-</span><span class="mi">1</span> <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">K</span><span class="p">)]</span>[m
[31m-[m
[31m-    <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">p_gifts</span><span class="p">)):</span>[m
[31m-        <span class="k">if</span> <span class="n">i</span> <span class="o">&gt;</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>[m
[31m-        <span class="k">else</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="mi">0</span>[m
[31m-[m
[31m-        <span class="n">loc</span> <span class="o">=</span> <span class="n">prev</span><span class="p">[</span><span class="n">p_gifts</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span>[m
[31m-        <span class="k">if</span> <span class="n">loc</span> <span class="o">!=</span> <span class="o">-</span><span class="mi">1</span><span class="p">:</span>[m
[31m-            <span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">]</span> <span class="o">=</span> <span class="nb">max</span><span class="p">(</span><span class="n">ret</span><span class="p">[</span><span class="n">i</span><span class="p">],</span> <span class="n">ret</span><span class="p">[</span><span class="n">loc</span><span class="p">]</span><span class="o">+</span><span class="mi">1</span><span class="p">)</span>[m
[31m-        <span class="n">prev</span><span class="p">[</span><span class="n">p_gifts</span><span class="p">[</span><span class="n">i</span><span class="p">]]</span> <span class="o">=</span> <span class="n">i</span>[m
[31m-[m
[31m-    <span class="k">return</span> <span class="n">ret</span><span class="p">[</span><span class="o">-</span><span class="mi">1</span><span class="p">]</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<p>두 코드는 정확히 같은 일을 한다. 두 가지의 부분문제를 결국 풀어낼 것이다. 첫 번째는 한 함수를 짜서 이 블락 안에서 두 문제를 모두 해결하며 두 번째는 각 부분문제마다 함수를 작성해서 최종적으로는 두 함수를 조합해 문제를 해결한다. 여기서 로직은 안 봐도 된다. 두 코드 중 어떤 형태가 바람직하다고 보는가?</p>[m
[31m-[m
[31m-<p><strong>내가 볼 때는 두 번째 코드가 훨씬 바람직하다고 본다.</strong> 그 이유는 다음과 같다.</p>[m
[31m-[m
[31m-<ul>[m
[31m-  <li><strong>각 기능에 대해 함수 단위로 뚜렷하게 구분되어 있어 가독성이 증대된다.</strong>[m
[31m-    <ul>[m
[31m-      <li>재사용성이 높은 코드는 가독성도 좋기 마련이다. 사실 이 포스트의 각 장은 조금씩 얽혀있는 부분이 있다.</li>[m
[31m-    </ul>[m
[31m-  </li>[m
[31m-  <li><strong>증대된 가독성 아래에서 필요한 문제 상황에 맞게 각 모듈을 필요할 때에 각각 사용할 수 있다.</strong>[m
[31m-    <ul>[m
[31m-      <li>앞서 말한 재사용성 높은 코드의 특징으로서 두 가지 부분기능 중 한 가지 기능만 필요할 수 있다. 이때 뚜렷하게 구분되어 있어 필요한 부분만 긁어가 바로 적용할 수 있다. 첫 번째 코드에서도 하려면 그렇게 할 수 있는데 각 영역 구분이 두 번째 코드처럼 뚜렷하지도 않고 잘 작성하지 않으면 두 가지 기능이 얽혀 이들을 분해해내기 매우 어려워질 수 있다.</li>[m
[31m-    </ul>[m
[31m-  </li>[m
[31m-  <li><strong>기타로서 변수명 등을 작성하기 더 쉬워진다.</strong> 결과 가독성이 추가로 증대된다.[m
[31m-    <ul>[m
[31m-      <li>첫 번째 코드 블락의 함수는 두 가지 일을 하기 때문에 이름 짓기가 까다롭다. 자신이 하는 일을 다 이름에 담으면 지나치게 길어지기 때문이다. 하지만 두 번째 코드에서는 각각의 기능을 따로 담았기 때문에 좀더 기능에 집중해 작명할 수 있다.</li>[m
[31m-    </ul>[m
[31m-  </li>[m
[31m-</ul>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>결론은 <strong>적재적소에 모듈성을 살린 기능 및 코드들은 전체 코드의 재사용성을 증대시키며 가독성까지 증대시키는 효과를 갖는다.</strong></p>[m
[31m-[m
[31m-<p><br id="4b" /></p>[m
[31m-[m
[31m-<h3 id="42-범용성">4.2. 범용성</h3>[m
[31m-[m
[31m-<p>범용성 또한 재미있는 주제다. <strong>범용성(generality)은 완전히 같은 프로그램을 보다 다양한 수요의 입력에 대응할 수 있도록 하는 코드의 특성을 이야기한다.</strong> 범용성 또한 코드의 재사용성과 관련된 중요한 요소다.</p>[m
[31m-[m
[31m-<p>범용성은 위보다 더 좋은 예제가 하나 있다. 바로 Fizzbuzz 문제로 숫자를 입력 받아 1부터 N까지 수를 순회하면서 3의 배수일 때는 ‘Fizz’, 5의 배수일 때는 ‘Buzz’, 15의 배수일 때는 ‘FizzBuzz’를 출력하도록 하는 문제다. 원래 이 문제는 북미에서 아이들이 나눗셈을 학습할 때 하는 미니게임 같은 것이라고 하는데 알고리즘을 처음에 학습할 때도 유용하게 해보는 문제기도 하다.</p>[m
[31m-[m
[31m-<p>순회하는 상환 N을 100이라고 할 때 코드는 다음과 같겠다.</p>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">101</span><span class="p">):</span>[m
[31m-    <span class="k">if</span> <span class="n">n</span> <span class="o">%</span> <span class="mi">3</span> <span class="o">==</span> <span class="mi">0</span> <span class="ow">and</span> <span class="n">n</span> <span class="o">%</span> <span class="mi">5</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-        <span class="k">print</span><span class="p">(</span><span class="s">'FizzBuzz'</span><span class="p">)</span>[m
[31m-    <span class="k">elif</span> <span class="n">n</span> <span class="o">%</span> <span class="mi">5</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-        <span class="k">print</span><span class="p">(</span><span class="s">"Buzz"</span><span class="p">)</span>[m
[31m-    <span class="k">elif</span> <span class="n">n</span> <span class="o">%</span> <span class="mi">3</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-        <span class="k">print</span><span class="p">(</span><span class="s">'Fizz'</span><span class="p">)</span>[m
[31m-    <span class="k">else</span><span class="p">:</span>[m
[31m-        <span class="k">print</span><span class="p">(</span><span class="n">n</span><span class="p">)</span>[m
[31m-[m
[31m-<span class="mi">1</span>[m
[31m-<span class="mi">2</span>[m
[31m-<span class="n">Fizz</span>[m
[31m-<span class="mi">4</span>[m
[31m-<span class="n">Buzz</span>[m
[31m-<span class="o">...</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<p>정말정말 무난한 Fizzbuzz 코드다. 아마 당신이 초심자로서 파이썬을 공부하면서 이 코드를 작성했다면 아마 칭찬을 들었을 것이다. 하지만 분명히 하자. 우리는 초심자로서 칭찬 듣자고 이 포스트를 보고 있지 않다.</p>[m
[31m-[m
[31m-<p>지금 이 코드는 범용성이 매우 낮은 코드다. 이유는 분명하다. 왜 나눗셈을 3과 5만 진행하는가? 4, 7, 11 등도 나눗셈을 할 수 있는 것 아닌가? 또 왜 ‘Fizz’, ‘Buzz’ 같은 단어를 출력하는가? 한국 사람인 나는 3으로 나눠질 때는 ‘울그락’, 5로 나눠질 때는 ‘불그락’을, 15로 나눠질 때는 ‘울그락불그락’을 출력하고 싶을 수도 있는 것이다.</p>[m
[31m-[m
[31m-<p>이런 문제상황이 현실세계에는 다분하다. 우리가 어떤 서비스를 운영할 때 수많은 유저들의 요구사항은 천차만별이기 마련이기 때문이다. 즉, <strong>여러 다양한 요소들과 함께 범용성 높은 코드를 작성하는 것도 중요하다.</strong> 만약 위와 같이 다양한 수요를 충족하는 FizzBuzz 코드를 작성한다면 보다 다양한 나눗셈 수요를 충족할 수 있을 것이고, 학생들은 나눗셈을 더 잘하게 될 것이다.</p>[m
[31m-[m
[31m-<p>이런 코드를 작성해보자.</p>[m
[31m-[m
[31m-<div class="language-python highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="k">def</span> <span class="nf">scalable_fizzbuzz</span><span class="p">(</span><span class="n">n</span><span class="p">,</span> <span class="n">items</span><span class="o">=</span><span class="p">((</span><span class="mi">3</span><span class="p">,</span> <span class="s">'Fizz'</span><span class="p">),</span> <span class="p">(</span><span class="mi">5</span><span class="p">,</span> <span class="s">'Buzz'</span><span class="p">))):</span>[m
[31m-    <span class="n">N</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">items</span><span class="p">)</span>[m
[31m-[m
[31m-    <span class="k">def</span> <span class="nf">generate</span><span class="p">(</span><span class="n">n</span><span class="p">,</span> <span class="n">i</span><span class="p">,</span> <span class="n">tmp_str</span><span class="p">):</span>[m
[31m-        <span class="k">if</span> <span class="n">i</span> <span class="o">==</span> <span class="n">N</span><span class="p">:</span>[m
[31m-            <span class="k">return</span> <span class="n">tmp_str</span> <span class="k">if</span> <span class="n">tmp_str</span> <span class="k">else</span> <span class="n">n</span>[m
[31m-[m
[31m-        <span class="n">divisor</span><span class="p">,</span> <span class="n">word</span> <span class="o">=</span> <span class="n">items</span><span class="p">[</span><span class="n">i</span><span class="p">]</span>[m
[31m-[m
[31m-        <span class="k">if</span> <span class="n">n</span> <span class="o">%</span> <span class="n">divisor</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-            <span class="n">ans</span> <span class="o">=</span> <span class="n">generate</span><span class="p">(</span><span class="n">n</span><span class="p">,</span> <span class="n">i</span><span class="o">+</span><span class="mi">1</span><span class="p">,</span> <span class="n">tmp_str</span><span class="o">+</span><span class="n">word</span><span class="p">)</span>[m
[31m-        <span class="k">else</span><span class="p">:</span>[m
[31m-            <span class="n">ans</span> <span class="o">=</span> <span class="n">generate</span><span class="p">(</span><span class="n">n</span><span class="p">,</span> <span class="n">i</span><span class="o">+</span><span class="mi">1</span><span class="p">,</span> <span class="n">tmp_str</span><span class="p">)</span>[m
[31m-        <span class="k">return</span> <span class="n">ans</span>[m
[31m-[m
[31m-    <span class="k">return</span> <span class="n">generate</span><span class="p">(</span><span class="n">n</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="s">''</span><span class="p">)</span>[m
[31m-[m
[31m-[m
[31m-<span class="n">N</span> <span class="o">=</span> <span class="mi">200</span>[m
[31m-<span class="n">length</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="nb">str</span><span class="p">(</span><span class="n">N</span><span class="p">))</span>[m
[31m-<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="n">N</span><span class="o">+</span><span class="mi">1</span><span class="p">):</span>[m
[31m-    <span class="c1"># Python string formatting: 다수의 출력을 깔끔하게 처리하기 위해 사용함.[m
[31m-</span>    <span class="k">print</span><span class="p">(</span><span class="n">f</span><span class="s">'{i:&lt;{length}} : {scalable_fizzbuzz(i, ((2, "짝"), (5, "오호라"), (7, "럭키세븐"))):&lt;20}'</span><span class="p">,</span> <span class="n">end</span><span class="o">=</span><span class="s">''</span><span class="p">)</span>[m
[31m-    <span class="k">if</span> <span class="n">i</span> <span class="o">%</span> <span class="mi">3</span> <span class="o">==</span> <span class="mi">0</span><span class="p">:</span>[m
[31m-        <span class="k">print</span><span class="p">()</span>[m
[31m-[m
[31m-<span class="mi">1</span>   <span class="p">:</span> <span class="mi">1</span>                   <span class="mi">2</span>   <span class="p">:</span> <span class="err">짝</span>                   <span class="mi">3</span>   <span class="p">:</span> <span class="mi">3</span>                   [m
[31m-<span class="mi">4</span>   <span class="p">:</span> <span class="err">짝</span>                  <span class="mi">5</span>   <span class="p">:</span> <span class="err">오호라</span>               <span class="mi">6</span>   <span class="p">:</span> <span class="err">짝</span>                   [m
[31m-<span class="mi">7</span>   <span class="p">:</span> <span class="err">럭키세븐</span>            <span class="mi">8</span>   <span class="p">:</span> <span class="err">짝</span>                   <span class="mi">9</span>   <span class="p">:</span> <span class="mi">9</span>                   [m
[31m-<span class="mi">10</span>  <span class="p">:</span> <span class="err">짝오호라</span>            <span class="mi">11</span>  <span class="p">:</span> <span class="mi">11</span>                   <span class="mi">12</span>  <span class="p">:</span> <span class="err">짝</span>[m
[31m-</code></pre></div></div>[m
[31m-[m
[31m-<p>보다 범용적인 FizzBuzz 기능을 함수로 만들었다. 다시 말해 모듈로 만들었다. 이 함수는 우리가 원하는 나눗셈 단위와 그때의 단어를 입력받을 수 있으며 난 어떤 수가 2, 5, 7로 나눠떨어질 때 각각 ‘짝’, ‘오호라’, ‘럭키세븐’의 단어를 붙여 출력하도록 했다.</p>[m
[31m-[m
[31m-<p>이 코드가 원래 Fizzbuzz 코드보다 어려운 것은 맞다. 하지만 분명한 것은 <strong>이 코드가 범용성이 높은 코드로서 이 기능을 Customizate 할 수 있어 훨씬 더 많은 유저를 만족시킬 수 있는 것이다.</strong> 그래서 만약 많은 유저가 사용하는 코드 또는 제품을 만들고 싶다면 이렇게 범용성을 고려한 코드를 짜야할 수도 있다.</p>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<p>정리하면 코드의 재사용성 또한 좋은 코드의 한 요소일 수 있고, 재사용성을 구성하는 주요 요소는 모듈성과 범용성이다. 모듈성은 한 기능(함수, 클래스) 등이 한 가지의 작업만 하도록 하는 것이고 이는 코드 전체의 재사용성을 높이고 보통 가독성에도 득이 된다. 다른 요소로는 범용성으로 범용성이 높은 코드는 같은 작업을 하더라도 보다 다양한 사용자의 수요를 널리 만족시킬 수 있어 자기만족 이상의, 사람들이 실제로 사용하는 프로그램의 중요한 요소가 된다.</p>[m
[31m-[m
[31m-<p><br />[m
[31m-<br id="5" /></p>[m
[31m-[m
[31m-<h2 id="5-구조화">5. 구조화</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br id="5a" /></p>[m
[31m-[m
[31m-<h3 id="51-용어-정의-구조화">5.1. 용어 정의: 구조화</h3>[m
[31m-[m
[31m-<p><br id="5b" /></p>[m
[31m-[m
[31m-<h3 id="52-코드-단위의-구조화">5.2. 코드 단위의 구조화</h3>[m
[31m-[m
[31m-<p><br id="5c" /></p>[m
[31m-[m
[31m-<h3 id="53-패키지-단위의-구조화">5.3. 패키지 단위의 구조화</h3>[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2>.</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2 id="-1">.</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2 id="-2">.</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2 id="-3">.</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2 id="-4">.</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<p><br /></p>[m
[31m-[m
[31m-<h2 id="-자료-출처">. 자료 출처</h2>[m
[31m-[m
[31m-<hr />[m
[31m-[m
[31m-<ul>[m
[31m-  <li><a href="https://www.sciencetimes.co.kr/?news=%EB%8B%AC-%ED%95%9C%EC%AA%BD%EB%A7%8C-%EB%B3%B4%EC%9D%B4%EB%8A%94-%EC%9D%B4%EC%9C%A0-%EC%9A%B0%EC%97%B0-%EC%95%84%EB%83%90">달 한쪽만 보이는 이유? 우연 아냐 - Sciencetimes</a></li>[m
[31m-  <li><a href="http://news.kbs.co.kr/news/view.do?ncd=4029990">페이스북 사용자 22억…유튜브와 위챗은? - KBS NEWS</a></li>[m
[31m-  <li>『알고리즘 문제 해결 전략』27장 ‘그래프의 표현과 정의’, 구종만, 인사이트(insight)</li>[m
[31m-  <li><a href="https://shoark7.github.io/programming/knowledge/unix-philosophy-intro">Unix philosophy - Parkito’s on the way</a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-  <li><a href=""></a></li>[m
[31m-</ul>[m
[31m-[m
[31m-<p>컴퓨터엔지니어를 위한 기술 영어작문</p>[m
[31m-[m
[31m-      <div class="page-footer">[m
[31m-        <div class="page-share">[m
[31m-          <a href="https://twitter.com/intent/tweet?text=내가 생각하는 '좋은 코드'란 바로 이런 것이다&url=http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are" title="Share on Twitter" rel="nofollow" target="_blank">Twitter</a>[m
[31m-          <a href="https://facebook.com/sharer.php?u=http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are" title="Share on Facebook" rel="nofollow" target="_blank">Facebook</a>[m
[31m-          <a href="https://plus.google.com/share?url=http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are" title="Share on Google+" rel="nofollow" target="_blank">Google+</a>[m
[31m-        </div>[m
[31m-        <div class="page-tag">[m
[31m-          [m
[31m-            <a href="/tags#good_code" class="tag">&#35; good_code</a>[m
[31m-          [m
[31m-            <a href="/tags#clean_code" class="tag">&#35; clean_code</a>[m
[31m-          [m
[31m-        </div>[m
[31m-      </div>[m
[31m-[m
[31m-			<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>[m
[31m-			<!-- 처음과끝에만 -->[m
[31m-			<ins class="adsbygoogle"[m
[31m-					 style="display:block"[m
[31m-					 data-ad-client="ca-pub-2670967175857332"[m
[31m-					 data-ad-slot="3352812061"[m
[31m-					 data-ad-format="auto"[m
[31m-					 data-full-width-responsive="true"></ins>[m
[31m-			<script>[m
[31m-					 (adsbygoogle = window.adsbygoogle || []).push({});[m
[31m-			</script>[m
[31m-			<!-- 처음과끝에만 -->[m
[31m-[m
[31m-		  <!-- Load Facebook SDK for JavaScript -->[m
[31m-  <div id="fb-root"></div>[m
[31m-  <script>(function(d, s, id) {[m
[31m-    var js, fjs = d.getElementsByTagName(s)[0];[m
[31m-    if (d.getElementById(id)) return;[m
[31m-    js = d.createElement(s); js.id = id;[m
[31m-    js.src = "https://connect.facebook.net/en_US/sdk.js#xfbml=1&version=v3.0";[m
[31m-    fjs.parentNode.insertBefore(js, fjs);[m
[31m-  }(document, 'script', 'facebook-jssdk'));</script>[m
[31m-[m
[31m-  <!-- Your share button code -->[m
[31m-  <div class="fb-share-button" [m
[31m-    data-href="http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are" [m
[31m-    data-layout="button_count">[m
[31m-  </div>[m
[31m-[m
[31m-		[m
[31m-    </div> <!-- End Wrap Content -->[m
[31m-  </div> <!-- End Page Content -->[m
[31m-</article> <!-- End Article Page -->[m
[31m-[m
[31m-</div>[m
[31m-[m
[31m-  </div>[m
[31m-[m
[31m-  <script>[m
[31m-  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){[m
[31m-  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),[m
[31m-  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)[m
[31m-  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');[m
[31m-  ga('create', '', 'auto');[m
[31m-  ga('send', 'pageview');[m
[31m-</script> <!-- End Analytics -->[m
[31m-[m
[31m-	<script src="https://unpkg.com/simple-jekyll-search@1.5.0/dest/simple-jekyll-search.min.js"></script>[m
[31m-<script>[m
[31m-var sjs = SimpleJekyllSearch({[m
[31m-  searchInput: document.querySelector('#search-input'),[m
[31m-  resultsContainer: document.getElementById('results-container'),[m
[31m-  json: '/search.json',[m
[31m-  searchResultTemplate: '<li class="search-results-item"><a href="http://localhost:4000{url}">{title}</a></li>',[m
[31m-	limit: 9,[m
[31m-	noResultsText: '<li class="search-results-item"><a href="#">No results found...</a></li>'[m
[31m-})[m
[31m-</script>[m
[31m-[m
[31m-	<!-- Main Js -->[m
[31m-<!--<script src="/assets/js/main.js"></script>-->[m
[31m-[m
[31m-<!-- JQuery 3.x min -->[m
[31m-<script src="/assets/js/jquery.js"></script>[m
[31m-[m
[31m-<script>[m
[31m-	let menus = $("#category-list");[m
[31m-	let image = $("#menu-toggler img");[m
[31m-	$("#toggler-wrapper").click(function() {[m
[31m-		if(menus.css("display") === "none") {[m
[31m-			image.attr("src", "/assets/img/close-button.png");[m
[31m-			menus.css("display", "flex");[m
[31m-		}[m
[31m-		else {[m
[31m-			image.attr("src", "/assets/img/nav-off.png");[m
[31m-			menus.css("display", "none");[m
[31m-		}[m
[31m-	});[m
[31m-[m
[31m-[m
[31m-</script>[m
[31m-[m
[31m-	<!-- Global site tag (gtag.js) - Google Analytics -->[m
[31m-<script async src="https://www.googletagmanager.com/gtag/js?id=UA-127149179-1"></script>[m
[31m-<script>[m
[31m-  window.dataLayer = window.dataLayer || [];[m
[31m-  function gtag(){dataLayer.push(arguments);}[m
[31m-  gtag('js', new Date());[m
[31m-[m
[31m-  gtag('config', 'UA-127149179-1');[m
[31m-</script>[m
[31m-[m
[31m-</body>[m
[31m-</html>[m
[1mdiff --git a/_site/search.json b/_site/search.json[m
[1mindex f0decb6..86bb862 100644[m
[1m--- a/_site/search.json[m
[1m+++ b/_site/search.json[m
[36m@@ -1,11 +1,11 @@[m
 [[m
   [m
     {[m
[31m-      "title"    : "내가 생각하는 &#39;좋은 코드&#39;란 바로 이런 것이다",[m
[32m+[m[32m      "title"    : "극소수 블로그 애독자들에게 고함",[m
       "category" : "",[m
[31m-      "tags"     : "good_code, clean_code",[m
[31m-      "url"      : "/programming/knowledge/this-is-what-good-codes-really-are",[m
[31m-      "date"     : "2019-12-31 00:00:00 +0900"[m
[32m+[m[32m      "tags"     : "",[m
[32m+[m[32m      "url"      : "/insight/rationality/inform-to-my-subscribers",[m
[32m+[m[32m      "date"     : "2020-02-09 00:00:00 +0900"[m
     } ,[m
   [m
     {[m
[1mdiff --git a/_site/sitemap.xml b/_site/sitemap.xml[m
[1mindex abe31a6..e14c3fd 100644[m
[1m--- a/_site/sitemap.xml[m
[1m+++ b/_site/sitemap.xml[m
[36m@@ -285,8 +285,8 @@[m
 <lastmod>2019-12-13T00:00:00+09:00</lastmod>[m
 </url>[m
 <url>[m
[31m-<loc>http://localhost:4000/programming/knowledge/this-is-what-good-codes-really-are</loc>[m
[31m-<lastmod>2019-12-31T00:00:00+09:00</lastmod>[m
[32m+[m[32m<loc>http://localhost:4000/insight/rationality/inform-to-my-subscribers</loc>[m
[32m+[m[32m<lastmod>2020-02-09T00:00:00+09:00</lastmod>[m
 </url>[m
 <url>[m
 <loc>http://localhost:4000/about.me</loc>[m
[1mdiff --git a/_site/tags/index.html b/_site/tags/index.html[m
[1mindex 1256505..d629a25 100644[m
[1m--- a/_site/tags/index.html[m
[1m+++ b/_site/tags/index.html[m
[36m@@ -460,9 +460,6 @@[m
     <li ><a href="#clean-code" class="tag">clean-code <span>(1)</span></a></li>[m
   [m
     [m
[31m-    <li ><a href="#clean_code" class="tag">clean_code <span>(1)</span></a></li>[m
[31m-  [m
[31m-    [m
     <li ><a href="#conditional-expression" class="tag">conditional-expression <span>(1)</span></a></li>[m
   [m
     [m
[36m@@ -496,9 +493,6 @@[m
     <li ><a href="#family" class="tag">family <span>(1)</span></a></li>[m
   [m
     [m
[31m-    <li ><a href="#good_code" class="tag">good_code <span>(1)</span></a></li>[m
[31m-  [m
[31m-    [m
     <li ><a href="#import" class="tag">import <span>(1)</span></a></li>[m
   [m
     [m
[36m@@ -1464,16 +1458,6 @@[m
     [m
   [m
     [m
[31m-  <h2 id="clean_code">clean_code</h2>[m
[31m-<!--  lists all posts corresponding to specific tag...-->[m
[31m-    [m
[31m-    <div class="tag-list">[m
[31m-        <span><a href="/programming/knowledge/this-is-what-good-codes-really-are">내가 생각하는 '좋은 코드'란 바로 이런 것이다</a></span>[m
[31m-        <small><span>| 31 Dec 2019</span></small>[m
[31m-    </div>[m
[31m-    [m
[31m-  [m
[31m-    [m
   <h2 id="conditional-expression">conditional-expression</h2>[m
 <!--  lists all posts corresponding to specific tag...-->[m
     [m
[36m@@ -1584,16 +1568,6 @@[m
     [m
   [m
     [m
[31m-  <h2 id="good_code">good_code</h2>[m
[31m-<!--  lists all posts corresponding to specific tag...-->[m
[31m-    [m
[31m-    <div class="tag-list">[m
[31m-        <span><a href="/programming/knowledge/this-is-what-good-codes-really-are">내가 생각하는 '좋은 코드'란 바로 이런 것이다</a></span>[m
[31m-        <small><span>| 31 Dec 2019</span></small>[m
[31m-    </div>[m
[31m-    [m
[31m-  [m
[31m-    [m
   <h2 id="import">import</h2>[m
 <!--  lists all posts corresponding to specific tag...-->[m
     [m
