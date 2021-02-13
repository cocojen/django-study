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

  ```
  [21, 18, 13, 10, 9, 5, 3]
  21 18 [13, 10, 9, 5, 3]
  ```

  이 코드는 더 짧고 더 읽기 쉽고, 인덱스로 인한 오류를 유발하지 않는다.

  

