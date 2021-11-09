# Collections 클래스에 대해 알아보자.
## Collections class ?
collections 클래스는 collection 인터페이스를 구현한 클래스에 대한 `객체생성`, `정렬` , `병합` , `검색` 등의 기능을 안정적으로 수행하도록 도와주는 역할을 하는 유틸리티 클래스이다.

이 메소드들은 제네릭 기술을 사용하여 작성되었으며 정적 메소드의 형태로 되어있다.
자주 사용하는 알고리즘으로는 `정렬` , `섞기` , `탐색` 등이 있다.

아래 표는 이 클래스의 메서드들이다.
![Alt Text]

## 예제
정렬
```
import java.util.*;

public class SortTest1 {
    public static void main(String[] args) {
        String[] example = { "Nice", "to", "meet", "you" };
        List<String> list = Arrays.asList(example); //배열을 리스트로 무조건 변환!
        Collections.sort(list); //리스트 정렬

        System.out.println(list);
    }
}
```
meet과 to의 위치가 바뀐 것을 볼 수 있다. 알파벳순이기 때문에 이러한 결과가 나온 것이다.


섞기
```
  import java.util.*;

public class Shuffle {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<Integer>();

        for(int i = 0; i <= 10; i++) {
            list.add(i);
        }

        Collections.shuffle(list);
        System.out.println(list);
    }
}
```

탐색
- 선형 탐색 : 처음부터 모든 원소를 방문하는 탐색 방법으로, 리스트가 정렬되어 있지 않은 경우 사용한다.

 

- 이진 탐색 : 리스트가 정렬되어 있는 경우 중간에 있는 원소(m)와 먼저 비교하여, 크면 그다음부(m+1)터 끝까지 비교하고, 작으면 처음부터 그 전(m-1)까지의 원소들과 비교하는 방식을 반복하여 하나의 리스트를 계속해서 두 개의 리스트로 분할한다. 이 방법은 리스트에 하나의 원소가 남을 때까지 반복된다. 이진 탐색은 문제의 크기를 반으로 줄일 수 있기 때문에 선형 탐색보다 효율적이다.
- Collections 클래스는 정렬된 리스트에서 지정된 원소를 이진 탐색한다. 



- 이진 탐색 메소드인 binarySearch()는 만약 반환값이 양수이면 찾고자 하는 원소의 인덱스값이고, 음수이면 탐색이 실패한 것이다. 즉, 원소를 찾지 못했음을 의미한다.

 
```
int index = Collections.binarySearch(list, element);

// list는 리스트, element는 탐색할 원소이다.
```
단, binarySearch() 메소드는 실패하더라도 도움이 되는 정보를 반환한다. 즉, 반환값에는 현재의 데이터가 삽입될 수 있는 위치 정보가 있다. 반환값이 pos라고 한다면, (-pos-1)이 해당 데이터를 삽입할 수 있는 위치이다.
```
int pos = Collections.binarySearch(list, key);

if(pos < 0) list.add(-pos-1);
```
binarySearch() 메소드는 위에도 언급했듯이 `정렬된 리스트`에 한해서 탐색을 진행한다는 점에 주의하여야 한다.

## 예제코드 및 참고
<a href = "https://velog.io/@gillog/Collections-%ED%81%B4%EB%9E%98%EC%8A%A4">Collections 클래스</a>
