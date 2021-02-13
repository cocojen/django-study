### Better way 13

- `슬라이싱` <<< `언패킹`

  예를 들어 다양한 값의 숫자로 이루어진 리스트가 있다고 했을 때, 그 중 가장 큰 숫자, 작은 숫자, 그리고 나머지 숫자들을 가져오는 코드를 짜야한다고 생각해보자.

  인덱스와 슬라이싱을 사용하는 것이 익숙한 방법이지만, **별표식** 을 사용하면 더욱 좋다. 

  ```python
  ages = [3, 13, 21, 5, 9, 10, 18]
  ages_descending = sorted(ages, reverse=True)
  print(ages_descending)
  oldest, second_oldest, *others = ages_descending
  print(oldest, second_oldest, others)
  ```

  -- 결과 --

  ```
  [21, 18, 13, 10, 9, 5, 3]
  21 18 [13, 10, 9, 5, 3]
  ```

  이 코드는 더 짧고 더 읽기 쉽고, 인덱스로 인한 오류를 유발하지 않는다.

  



### Better way 14

- 복잡한 기준을 사용해 정렬할 때는 key 파라미터를 사용해라

  - list 에는 sort 메서드가 들어 있다. 기본적으로 sort는 원소 타입에 따라 자연스러운 순서로 오름차순으로 정렬한다.

  - 당연히 숫자나, 스트링 값은 정렬이 쉽다. 하지만 내가 만든 객체를 어떤 값에 의해 정렬하고 싶을때는 어떻게 할 수 있을까?

  - 이때는 지금까지는 사용하지 않았지만 sort메서드가 가지고 있는 키 파라미터를 이용하자. ( **sort** 에 **key**  라는 파라미터가 있다)  key 는 함수여야 하고, key 함수에는 정렬 중인 리스트의 원소가 전달 된다. key 함수가 반환하는 값은 원소 대신 정렬 기준으로 사용할, 비교 가능한 값이어야만 한다.

  - 다음 예제는 람다 키워드로 함수를 정의했다. 이 함수를 키로 사용하면 블랙핑크 `객체`로 이뤄진 리스트를 age에 따라 정렬한다.

    ```python
    class Blackpink:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def __repr__(self):
            return f'member({self.name!r}, {self.age})'
    
    Jisoo = Blackpink('Jisoo', 27)
    Jennie = Blackpink('Jennie', 26)
    Rose = Blackpink('Rose', 25)
    Lisa = Blackpink('Lisa', 25)
    
    members = [
        Jisoo,
        Jennie,
        Rose,
        Lisa
    ]
    
    print('미정렬:', repr(members))
    members.sort(key=lambda x: x.age)
    print(f'나이 순 정렬:', members)
    members.sort(key=lambda x: x.name)
    print(f'이름 순 정렬:', members)
    ```

    -- 결과 -- 

    ```
    미정렬: [member('Jisoo', 27), member('Jennie', 26), member('Rose', 25), member('Lisa', 25)]
    나이 순 정렬: [member('Rose', 25), member('Lisa', 25), member('Jennie', 26), member('Jisoo', 27)]
    이름 순 정렬: [member('Jennie', 26), member('Jisoo', 27), member('Lisa', 25), member('Rose', 25)]
    ```

    - 그냥 출력했을 때는 members 리스트에 들어있는 순서대로 출력이 되었고, sort함수의 키에 객체들의 age 를 넘겨주었더니 오름차순으로 정렬이 되었다.

      

