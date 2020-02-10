2020.02.10 Fooddeuk Project



## 1. 같은 페이지에 각각 다른 jQuery 버전 적용하기

### jQuery different versions on same page 



이미 잘 만들어져있는 라이브러리들을 가져오다보면 필연적인 많은 오류들이 생긴다. 그 중에 가장 흔한 오류는 바로 버전문제! python이든 jQuery든 각각 라이브러리가 만든 시점의 버전이 다르기 때문에 세세한 오류들이 발생하여 구동할 수 없게 만든다. 



이 때, 생각해 낸것이 같은 페이지라도 jquery 버전을 다르게 줄 는 방법을 생각해보게 되었다. 



- 검색 결과 

```js
<!-- load jQuery 1.1.3 -->
<script type="text/javascript" src="http://example.com/jquery-1.1.3.js">
</script> 
<script type="text/javascript">
var jQuery_1_1_3 = $.noConflict(true);

//cdn 방식으로 불러온 jquery를 $.noConflict(true);을 이용하여 jQuery_1_1_3 이라는 명칭으로 저장한다. 

</script>

<!-- load jQuery 1.3.2 -->
<script type="text/javascript" src="http://example.com/jquery-1.3.2.js"></script>
<script type="text/javascript">
var jQuery_1_3_2 = $.noConflict(true);
// jQuery_1_3_2 다른이름으로 버전 불러와 저장.
</script>
```







- 실제 적용

```js
<!-- jQuery Mobile -->
<link rel="stylesheet" href="http://code.jquery.com/mobile/1.3.2/jquery.mobile-1.3.2.min.css" />
<script src="http://code.jquery.com/jquery-1.9.1.min.js"></script>
<script src="http://code.jquery.com/mobile/1.3.2/jquery.mobile-1.3.2.min.js"></script>

<!-- jQuery $311 -->
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<script>
var $j311 = jQuery.noConflict();
</script>
```

사용하려던 라이브러리는 jQuery 3.1.1버전을 이용 하였고, 우리는 모바일 버전의 웹 애플리케이션을 만들려고 하였기에 두 버전간의 충돌이 필연적으로 일어날 수 밖에 없던 상황이다. 



> jQuery 3.1.1 =! jQuery 1.9.1 

일단 이런 형식의 $.noConflict(true); 문법을 사용하기 위해서는 각 버전의 JS를 수정해야한다. 예를들어 



```js
$j311 = jQuery.noConflict();
// $j191 = jQuery.noConflict();
// cdn 방식으로 불러온 jquery는 수정할 수가 없어서 그냥 씀.
```



이렇게 수정하였다면, 이버전에 사용된 자바스크립트들을 사용 할때 $j311을 써줘야한다.



```js
$j311("#signin").click(function () {
      $("form").submit();
      return false;
    });
```



그렇다는건 각 라이브러리에 쓰인 js파일에 버전별로 j311로 바꿔야지 문제가 없이 실행 될 수있다.



```js
;(function ($, window, document, undefined) {
	var pluginName = "lib",
		defaults = {
			onDislike: null,
			onLike: null,
			animationRevertSpeed: 200,
			animationSpeed: 400,
			threshold: 1,
		};
		.
		.
		.
		
})($j311, window, document);
 //(jquery, window, document); > ($j311, window, document);
```

이름을 바꿀 때, 한가지 팁을 주자면 js파일 맨 마지막에만 바꾸면 된다.  







참고자료 : https://stackoverflow.com/questions/1566595/can-i-use-multiple-versions-of-jquery-on-the-same-page