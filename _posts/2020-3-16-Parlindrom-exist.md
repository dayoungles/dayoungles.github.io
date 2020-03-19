---
layout: post
title: Palindrome permutation
categories: [Leetcode]
---

오늘의 알고리즘은 주어진 문자열의 순열이 palindrome(회문: 수박수박수)을 구성할 수 있는가 하는 문제였다.

헷갈려서 solution을 확인했는데, 나는 "permutation of the string could form a palindrome" 이라는 부분을 스트링의 일부가 회문 형식으로 구성될 수 있느냐는 것으로 이해해버림. Permutation에 대한 내용을 무시해버린 것이다. 덕분에 상당한 시간을 삽질에 쏟았고, 이게 easy레벨이야?ㅠㅠ하면서 솔루션을 확인했다.
확인 결과 우선 문제를 잘못 이해했음을 깨달았고, 내용을 읽으면서 이미 답을 봐 버렸기 때문에 실제로 코드를 짜는 시간은 오래 걸리지 않았다.
주어진 문자열의 순열이 회문이어야 하기 때문에 해당하는 경우는 두 가지 뿐이다. 전체 문자열의 캐릭터가 각각 2개씩 쌍을 이루고 있거나, 오직 하나의 홀수 캐릭터를 가지고 있거나.

```
"aba" -> 홀수인 캐릭터 b가 하나 뿐이니 가능
"aabbaa" -> 전체가 짝수이니 가능
"abc" -> 홀수인 캐릭터가 세개라서 불가능
"ab" -> 홀수인 캐릭터가 두개라서 불가능
```

#### Space complexity
HashMap에 집어넣고 카운트를 하면서 전체 문자열의 길이만큼 공간을 확보(O(n))

#### Time complexity
HashMap에 집어넣는데 O(n), 다 집어넣고 나서 foreach문을 돌면서 다시 짝/홀수 여부를 확인해야 하기 떄문에 여기서도 최악의 경우 O(n). 최대 O(n)

작성한 코드는 요기에: [my leetcode repo](https://github.com/dayoungles/leet_code/commit/eab56ddeb6cf26225a051dffb2d2a43d68157ddd#diff-1acd20410396659c149d5b1b45f147c9)



[References]
[Leet code: ](https://leetcode.com/problems/palindrome-permutation/)