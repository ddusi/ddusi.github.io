---
layout: post
title: jQuery mobile $.mobile.changePage 
date: 
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: how-to-start.jpg # Add image post (optional)
tags: [Programming, Learn] # add tag
---



2020-02-10-jQuery mobile $.mobile.changePage 



## $.mobile.changePage를 썼는데 페이지 로딩이 안되요!

### jquery mobile changepage reload page not working



​	jquery mobile을 처음 써보는 생 초짜인 저로선, 이 당연한 것도 몰랐다. 일단 changePage함수의 속성들를 다 주어도 페이지가 이동했을때, 내가 쓴 데이터들이 화면에 출력이 되지 않았다. 



- changepage 속성들을 적용

```JS
$(".right-button").on("click", function() {
  $.mobile.changePage("/right", {
    allowSamePageTransition : true,
    transition: "slide",
    type: "get",
    showLoadMsg: false,
    reloadPage: true
  });
});
```



이때, 나는 페이지를 이동하여도 페이지가 리로딩이 되지 않아서 발생하는 오류가고 생각 했지만,  생각보다 기본적인 오류였다. 



- jquery mobile의 기본 원리

​	mobile jQuery는 작동할 때, HTML5 방식으로 작동된다. 즉 ,유동적인 페이지관리이기 때문에 태header, footer, navigetor, container, content 와 같은 태그명과 클래스명으로 유동적으로 작동한다. 이 때, 꼭 모든 페이지의 요소가 로딩되려면 `<div data-role="page">` 형식으로 감싸줘야한다.

```html
<body> 
<div data-role="page">
    
    <header></header>
    <div class="container">
        <div class="content">

        </div>
    </div>
    <footer></footer>
    <script></script>
    
</div>
</body>
```

이 때, script들도 그대로 묶어줘야 페이지 이동시 리로딩이 작동한다!

다른분들은 저같은 삽질은 피하기 위해...





참고: https://stackoverflow.com/questions/23672232/jquery-mobile-change-page-does-not-reload-page



