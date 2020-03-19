---
layout: post
title: Jewels and Stones
categories: [Leetcode]
---

오늘의 알고리즘은 String 2개가 주어진 상태에서 J에 포함되어 있는 character가 S에 몇번 존재하는지를 확인하는 것이었다.

제일 첫 번째 시도는 HashMap을 이용, S의 char을 하나씩 map에 집어넣으면서 value를 하나씩 ++ 시켜주었다. 그리고 J의 for loop을 돌면서 해당하는 키가 map에 존재하는지 확인하고 map에 있으면 값을 더해서 돌려주는 것으로. 첫 번쨰 시도에서 submit에 성공했으나 메모리 사용 수준이 95% 순번이라 수정해보기로 했다. 
```java 
	Map<Character, Integer> stoneMap = new HashMap<>();

        for (int i = 0; i < S.length(); i++) {
            stoneMap.put(S.charAt(i), stoneMap.getOrDefault(S.charAt(i), 0)+1);
        }
        int count = 0;

        for (int i = 0; i < J.length(); i++) {
            count += stoneMap.getOrDefault(J.charAt(i), 0);
        }

        return count;
```

solution을 확인해보니 map이 아니라 set을 사용해서 contains로 확인하는 케이스가 있었다.  set에 J캐릭터를 모두 넣고 S를 돌면서 있는지 확인하고 contains true가 나오면 넘어가는 것. 메모리를 줄이는데는 도움이 되지 않았다.

```java
	Set<Character> set = new HashSet<>();
        int result = 0;
        for (char c: J.toCharArray() ) {
            set.add(c);
        }
        for (char s : S.toCharArray()) {
            if(set.contains(s)) result++;
        }
        return result;
```

마지막 시도였으나 역시 메모리를 줄이는데 도움이 되지는 않았다. 하지만 속도가 빨라졌다. Hashmap을 쓰지 않아서 그런 것 같다. S를 돌면서 J의 해당 캐릭터 인덱스가 없으면 (== -1)  넘어가는 것. 

```java
	int count = 0;
        for (char c : S.toCharArray()) {
            if(J.indexOf(c) != -1) count++;
        }
        return count;
```

#### Space complexity
hash를 쓰는 방법으로는 S or J의 크기만큼 map 공간을 사용하게 되니 O(n)
세번쨰 방법은 주어진 J와 S를 그대로 쓰고 새로운 공간을 사용하지 않기 때문에 O(1)

#### Time complexity
Hash를 쓰는 방식은 O(J+S) for 문을 두번 다 도는 것 밖엔 답이 없다. 
하지만 마지막 방법은 O(S)

작성한 코드는 요기에: [my leetcode repo](https://github.com/dayoungles/leet_code/blob/0ea59e9500298c43b6eb3f724f6a0b9ffbee9555/src/leet/NewJewelsInStones.java)

[References]
[Leet code problems](https://leetcode.com/problems/jewels-and-stones/)