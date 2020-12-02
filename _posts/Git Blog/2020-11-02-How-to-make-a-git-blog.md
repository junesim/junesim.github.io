---

title: How to make a git blog
categories: [깃 블로그 만들기]

---

&nbsp;&nbsp;깃 블로그를 만들어보자.

&nbsp;&nbsp;깃 블로그를 만드는 방법은 매우 쉬워보이고 실제로 쉽기도 하다.
&nbsp;&nbsp;모두가 가지고 있는 블로그를 생성해보고 원하는 것을 공유해보자!

&nbsp;&nbsp;구름IDE와 Jekyll를 이용해 블로그를 생성해보겠다.
일단 Github에서 레포지토리 이름을 <strong>username</strong>.github.io로 생성 해주자. 꼭 위 방법대로 생성할 필요는 없다. 자신이 원하는 이름으로 레포지터리를 생성한 뒤 설정에서 깃허브 페이지 설정을 지정해 페이지를 생성할 수 있다. 
![example_gitsettings](/img/ex_post_1/ex1_gitsettings.png)

&nbsp;&nbsp;레포지터리를 생성한 후 README.MD에 글을 쓴 후 <strong>username</strong>.github.io에 접속 시 README의 내용이 바로 출력되는 것을 확인할 수 있다. 

![example_website](/img/ex_post_1/ex2_web.png)

&nbsp;&nbsp;이렇게 하면 기초적인 설정은 끝났다. 이제 테마를 이용해 블로그의 레이아웃을 생성해보자.Jekyll의 경우에는 정말 많은 테마들이 있는데, 이 블로그의 경우에는 [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes) 테마를 이용해 작성됐다. 많은 분들이 이 테마를 이용해 자료가 많기 때문에 처음에 블로그를 생성하는 분들에게 추천드린다. 

&nbsp;&nbsp;위 깃을 클론하고 이를 자신이 만든 레포지터리에 커밋하면 테마가 적용된다. 여기서 config.yml을 수정해서 사이트를 설정해주면 되는데, 먼저 URL과 Author 부분을 설정해주도록 하자. 
 
 
&nbsp;&nbsp;현재 깃에서 직접 수정하고 반영하는 경우 블로그의 수정을 확인하려면 매번 커밋이 이루어져야 한다. 따라서 보통 수정한 후 루비를 이용해 로컬에서 확인하고 수정하는데, 다음 포스트에서는 이를 구름을 이용해 하는 것을 이야기 해 보겠다.