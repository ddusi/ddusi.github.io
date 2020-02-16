2020-02-16-jQuery Mobile 설치, 간단한 기능 설명



##  jQuery mobile 설치 간단한 기능

### how to ues jquery mobile 



### 1. 설치하기

- 파일 직접 다운로드

https://jquerymobile.com/download/



- Copy-and-Paste snippet for jQuery CDN hosted files: 

```html

<link rel="stylesheet" href="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.css" />
<script src="http://code.jquery.com/jquery-1.11.1.min.js"></script>
<script src="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.js"></script>

```





### 2. 기본 구조

index.html

```html
<body>
    <!-- 페이지 1 번 -->
    <section id="page1" data-role="page">
        <header data-role="header"><h1>jQuery Mobile</h1></header>                   
        <div class="content" data-role="content">
            <p>1 page</p>
            <p><a href="#page2">go page2</a></p> 
            <p><a href="externalPage.html" data-ajax="false">go external page</a></p> 
        </div>
        <footer data-role="footer"><h1>footer</h1></footer>
    </section>
     
    <!-- 페이지 2번 -->
    <section id="page2" data-role="page">
        <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile</h1></header>
        <div class="content" data-role="content">
            <p>2 page</p>
            <p><a href="#page3">go page3</a></p>
        </div>
        <footer data-role="footer"><h1>footer</h1></footer>
    </section>
     
    <!-- 페이지 3번 -->
    <section id="page3" data-role="page">
        <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile</h1></header>
        <div class="content" data-role="content">
            <p>3 page</p>
            <p><a href="#page1">go page1</a></p>
        </div>
        <footer data-role="footer"><h1>footer</h1></footer>
    </section>
</body>
```



제이쿼리 모바일은 기본적으로 한 페이지 안에서 여러 페이지를 나눠서 작성할 수 있다. 위의 코드를 살펴보면 3개의 페이지를 한번에 뿌리고 관리한다. 

제이쿼리 모바일은 커스텀 태그 속성인 data-role을 이용하여 역할을 인식한다. 그러므로 꼭 각 속성별로 속성을 지정해줘야한다.  







### 3. jQuery Mobile Layout

![img](2020-02-16-모바일 제이쿼리.assets/f0165519_5106a6aa9a07a.png)





- data-role 속성들

  \- **data-role** : html5의 data-* 태그로, jQueryMobile에서는 Layout 을 설정하는데 사용된다.

  \- **page** : 모바일 브라우저에 표시되는 하나의 페이지

  \- **header** : 페이지의 Header 영역. 페이지 상단에 Toolbar 형태로 표현됨

  \- **content** : 실제 콘텐츠가 표시되는 영역

  \- **footer** : 페이지의 Footer 영역. 페이지 하단에 Toolbar 형태로 표현됨

  \- **data-position** : Layout 의 위치를 지정하는데 사용된다 "fixed"로 지정한 경우, 화면 하단의 고정위치로 표시된다.

  그외 속성들 https://api.jquerymobile.com/data-attribute/





- data-role의 포함관계

  data-role="page"
    └> data-role="header"
    └> data-role="content"
    └> data-role="footer"



> 항상 page 에 포함되어있는 구조로 만들어야 한다!
>
> 이 page는 중첩할수 없으며 항상 body의 자식이여야 한다.





### 4. 외부 페이지로 직접 이동.

먼저 외부페이지를 만든다 



**externalPage.html**

```html
<body>
 
<section id="page4" data-role="page">
    <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile External Page</h1></header>                   
    <div class="content" data-role="content">
        <p>external 1 page</p>
        <p><a href="#page5">go external page5</a></p>
        <p><a href="#page2">go page2</a></p>
    </div>
    <footer data-role="footer"><h1>footer</h1></footer>
</section>
 

<section id="page5" data-role="page">
    <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile External Page</h1></header>
    <div class="content" data-role="content">
        <p>external 2 page</p>
        <p><a href="#page6">go external page6</a></p>
    </div>
    <footer data-role="footer"><h1>footer</h1></footer>
</section>
 

<section id="page6" data-role="page">
    <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile External Page</h1></header>
    <div class="content" data-role="content">
        <p>external 3 page</p>
        <p><a href="#page4">go external page4</a></p>
    </div>
    <footer data-role="footer"><h1>footer</h1></footer>
</section>
 
</body>
```





이 외부페이지를 불러오는 방법이 있는데, index.html에서 두가지의 상황을 사용해보자.

1. 비동기로 미리 불러와 외부페이지를 로딩시켜놓을 수 있지만, 외부 페이지 간의 이동은 어렵다.

   - 비동기로 불러오는 방법 

     ```html
     <a href="externalPage.html" data-prefetch="true">go external page</a>
     ```

2. 직접 외부페이지로 이동하는 방법 

   - 비동기와 달리 직접 위치가 움직이기 때문에 외부 페이지간의 이동 자유

     ```html
     <p><a href="externalPage.html" data-ajax="false">go external page</a></p>
     ```







### 5. 페이지 이벤트

jquery mobile은 비동기 방식이므로 페이지를 로딩하는 이벤트와 로딩하기 전 후 이벤트를 구별합니다. jquery에서는 보통 ready 메소드를 사용하여 jquery(douvument).read(); 또는 약식으로 $(function(){}); 으로 사용하기도 합니다.



**pagebeforehide**

a 페이지에서 b 페이지로 이동하기 전에 a 페이지에서 발생하는 이벤트 입니다. ui.nextPage는 이동할 페이지 b 이며 b가 없을 경우에는 빈 jquery 객체입니다.

 

**pagebeforeshow**

a 페이지에서 b 페이지로 이동하기 전에 b 페이지에서 발생하는 이벤트 입니다. ui.prevPage는 이동 시작 페이지 a 이며 a가 없을 경우에는 빈 jquery 객체입니다.

 

**pagehide**

전환 시작 페이지 a 에서 전환이 끝난 후 발생합니다. ui.nextPage는 전환대상 페이지의 jquery 객체이며 전환 대상 페지이가 없을 경우는 빈 객체입니다.

 

**pageshow**

전환 대상 페이지 b 에서 전환이 끝난 후 발생합니다. ui.prevPage는 전환 시작 페이지의 jquery 객체이며 전환 시작 페이지가 없을 경우는 빈 객체입니다.



이벤트를 사용하려면 적당한 이벤트 리스너를 사용해야 합니다.

**jquery.bind(), jquery.delegate(), jquery.on()** 을 써서 사용할 수 있습니다.

 

보통은 bind를 사용해도 무방하지만 비동기로 불러온 페이지에는 delegate나 on을 사용해야 합니다.



```html
    <head>
    <script type="text/javascript">
    $(function(){
        $("#page1").bind("pagebeforehide",function(event, ui){
            alert("1페이지에서 2페이지로 전환 전에 1페이지에서 작동합니다.");
        });

        $("#page2").bind("pagebeforeshow",function(event, ui){
            alert("1페이지에서 2페이지로 전환 전에 2페이지에서 작동합니다.");
        });

        $("#page1").bind("pagehide",function(event, ui){
            alert("1페이지에서 2페이지로 전환이 끝난 후에 1페이지에서 작동합니다.");
        });

        $("#page2").bind("pageshow",function(event, ui){
            alert("1페이지에서 2페이지로 전환이 끝난 후에 2페이지에서 작동합니다.");
        });

        ///////////////////////////////////////////////////////////////////////////

        $("#page2").bind("pagebeforehide",function(event, ui){
            alert("2페이지에서 1페이지로 전환 전에 2페이지에서 작동합니다.");
        });

        $("#page1").bind("pagebeforeshow",function(event, ui){
            alert("2페이지에서 1페이지로 전환 전에 1페이지에서 작동합니다.");
        });

        $("#page2").bind("pagehide",function(event, ui){
            alert("2페이지에서 1페이지로 전환이 끝난 후에 2페이지에서 작동합니다.");
        });

        $("#page1").bind("pageshow",function(event, ui){
            alert("2페이지에서 1페이지로 전환이 끝난 후에 1페이지에서 작동합니다.");
        });

        ///////////////////////////////////////////////////////////////////////////

    });
    </script>
</head>
<body>
 
<section id="page1" data-role="page">
    <header data-role="header"><h1>jQuery Mobile</h1></header>                   
    <div class="content" data-role="content">
        <p>1 page</p>
        <p><a href="#page2">go page2</a></p>
    </div>
    <footer data-role="footer"><h1>footer</h1></footer>
</section>
 
<section id="page2" data-role="page">
    <header data-role="header" data-add-back-btn="true"><h1>jQuery Mobile</h1></header>
    <div class="content" data-role="content">
        <p>2 page</p>
        <p><a href="#page1">go page1</a></p>
    </div>
    <footer data-role="footer"><h1>footer</h1></footer>
</section>
 
</body>
```



