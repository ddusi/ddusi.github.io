2020-02-17-z-index가 적용이 안되요!





## Z-index가 적용이 안되요! 

### z-index is not working!



프로젝트를 하면서 z-index때문에 아주 골머리를 썩힌적이 있었다. 이때, 하위 요소에 아무리 높은 인덱스를 줘도 적용이 안되는 것에 너무 많이 힘들었다. 그러므로 나같은 삽질을 피하라고 올린다. 



#### 1. z-index의 알고리즘? 

z-index의 순서는 생각보다 그리 간단하지 않다. 아직까지도 정확하게는 이해하지 못했지만 결과론적으로 알게된 사용법만 익히면 문제될게 없다고 생각된다. 



#### 2. z-index를 사용하기 위해선?

​	**position 속성을 부여해줘야 한다. (static 제외)**



#### 3. z-index가 기본적으로 쌓이는 순서

<img src="2020-02-17-z-index에 영향을 주는 opacity.assets/new-stacking-order.png" alt="new-stacking-order" style="zoom: 67%;" />

z-index는 숫자가 클 수록 위에 쌓인다는 개념으로 보면 된다. 그리고 음수도 가능하다.

z-index나 position 속성이 없을 경우 일반적으로 html의 순서대로 쌓인다. 





#### 4. z-index에 영향을 주는 것들?? 

- opacity

  opacity라는 스타일은 불투명도를 조정하는 스타일이다. 근데 이게 아이러니하게도 z-index에 영향을 준다!

  ```css
  div:first-child {
  	opacity:.99;
  }
  ```

  위 코드대로 z-index를 쓰지 않고도 두번째 위치로 옮길 수가 있다. 



- Stacking contexts (쌓임 맥락)

  같은 부모를 두어 쌓임 순서에 따라 한꺼번에 움직일 수 있는 요소들을 쌓임 맥락이라고 한다. 이 쌓임맥락에 얽혀있는 요소는 부모 범위를 벗어나지 못하게 한계를 정하게 된다. 아무리 z-index를 줘도 빠져나올 수가 없다는 뜻.

  

  그렇다면 이 쌓임 맥락은 언제 만들어질까? 

  

  **쌓임맥락이 만들어지는 경우**

  - 요소가 문서의 뿌리요소일 때 (즉, `<html>` 요소)
  - 요소의 position 값이 `static`이 아니면서 `z-index`도 `auto`가 아닐 때
  - 요소의 opacity 값이 1보다 작을 때



#### 5. 쌓임맥락에서 손쉽게 빠져나오는 법

​	정확하게 어떻게 되는 알고리즘인지는 모르지만, 쌓임맥락으로 묶여있을 때, 하위 요소에 position을 fixed로 주면 빠져 나올 수 있는 것을 알게 되었다.

````css
{
    position : fixed;
}
````







참고:https://mytory.net/archives/10997

참고2: https://tympanus.net/codrops/css_reference/z-index/





 




