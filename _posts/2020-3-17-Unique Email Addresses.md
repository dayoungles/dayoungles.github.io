---
layout: post
title: Unique Email Addresses
categories: [Leetcode]
---

오늘의 알고리즘은 email로 구성된 String 리스트를 주고, dot(.)과 plus(+) 기호의 예외 처리를 한 후 실제 unique한 email 주소의 개수를 리턴하는 것이었다.

email 주소라서 왠지 친근한 감이 있었다. java String의 split과 replace를 사용해서 처리했다. 첫 제출에 실수가 있었는데, 도메인을 따로 떼어놓지 않고 계속 같이 스트링에 넣어둔 상태로 사용해서 그런 것.
foreach를 돌면서 전체 리스트를 순회, 각 email주소에서 도메인을 뜯어내고, .과 +를 대체하는 작업을 완료 후 미리 선언해둔 HashSet에 저장해서 중복을 처리하고 최종적으로는 HashSet의 크기로 값을 리턴.

```java

for (String email :emails) {
    sb.delete(0, sb.length());
    String[] parts = email.split("@");
    String withoutPlus= parts[0].split("\\+")[0];
    sb.append(withoutPlus.replace(".", ""));
    sb.append("a");
    sb.append(parts[1]);
    hset.add(sb.toString());

}
```
split은 regex를 사용하기 때문에 성능이 좋지 않다는 말도 있지만 손에 익은 함수가 최선이라고 생각했다.
replace는 다시 확인해보니 안에서 replaceAll을 호출하고 while문을 돌기 때문에 직접 구현해도 다를 바가 없다고 생각해서 유지했음.
나중에 성능이 썩 좋진 않아서(상위 30프로 정도) 수정하려고 해봤지만 내 코드로는 더 개선이 어려웠다. 솔루션을 확인하니 **String buffer**가 있어서, 사용했더니 성능 개선!

#### Space complexity
HashSet에 add하기 때문에 최대 전체 String 배열의 길이만큼 공간을 사용(O(n))

#### Time complexity
foreach에서 O(n)(주어진 리스트의 길이만큼 순회),
매 foreach에서 첫번째 split에서 O(해당 문자열.length)
매 foreach에서 두번째 splitdㅔ서 O(해당 문자열의 주소 부분의.length)
매 foreach에서 replace하면서 (해당 문자열의 주소부분의 length)

이러면 O(n)으로 해도 될듯.

작성한 코드는 요기에: [my leetcode repo](https://github.com/dayoungles/leet_code/blob/master/src/leet/NumUniqueEmails.java)

[References]
[Leet code problems](https://leetcode.com/problems/unique-email-addresses/)