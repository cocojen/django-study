### # Model

>  `챕터 6` (63p ~)

---



### 하나의 앱에 모델이 20개 이상이면 작은 앱으로 쪼개라.

- 앱 하나 당 5~10개 정도의 모델을 가지고 있는 것이 좋다.

  (나는 앱이 아니라 프로젝트 전체에서 사용되는 앱이 20개도 안돼서 이런 경우가 없었지만ㅋㅋ 모델이 너무 많아지면 쪼개자 당연한 소리..)

---





### 모델 상속시 주의하기

- 장고에서는  `abstract base classes`, `multi-table inheritance`, `proxy models`   세 가지 모델 상속 타입을 제공한다.





	> 이 책에서는 실습 부분이 abstract base class 밖에 없고 , 공식문서 링크에서 더 많은 것을 참조하라고 나와있다. 나는 이 책의 하나가 흐름을 잘 이해하지 못하겠다.. 보통 세 가지 있다고 하면 세 가지 다 실습해줘야하지 않나?? 하나 알려주고 나머지는 공식문서 보라고하면 어쩌라는 것? 그럼 하나도 알려주지 말고 세 가지 다 공식문서 보라 고하지?? 어쨌든 나는 하나만 실습하고 가기는 찝찝하기 때문에 내가 알아서 세 가지 실습을 하고 정리하겠다. 



  #### Model Inheritance 실습

#### 	1. Abstract base classes

  - abstract parent 클래스가 다른 모델에서 사용될 공통적인 필드를 가지고 있으면, 우리가 타이핑하는 것을 줄여준다

  - 실례로, 모델에 `created` , `modified` 필드를 넣는 것은 정말 흔하다. 일일이 모든 모델에 이 필드들을 추가할 수도 있지만, 더 좋은 방법이 있다.

    

    ![abstract base class 실습](Model.assets/abstract_base-0262021.jpg)

    

- 위와 같이 TimeStampedModel 를 만들고 abstract base class 로 정의해주면, 장고는 migrate 할 때 이 클래스의 테이블을 생성하지 않는다.

- 위의 예시에서는 세 가지 테이블이 아니라, 두 가지 테이블, Post, Comment만 생성된다. 

- Parent 클래스의 필드들이 Child class인 Post와 Comment에 (created, modified)  추가되었다.

  

  <img src="Model.assets/abstract_base_table.png" alt="스크린샷 2021-01-10 오후 4.06.06" style="zoom: 50%;" />



---



### 2. Multi-table-inheritance 

### 3. Proxymodels



