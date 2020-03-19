---
layout: post
title: Find Anagram Mappings
categories: [Leetcode]
---

오늘의 알고리즘은 주어진 array 2개를 비교하여 두 번째 배열의 아이템이 첫 번째 배열의 몇 번째 아이템이었는지 각각 확인하고 순서를 다시 int 배열로 만드는 것이었다.

HashMap을 이용, for loop을 돌면서 두번째 array의 순서를 item:array number 형식으로 저장하고 다시 첫번째 배열을 for loop을 돌면서 해당 item의 값을 hashmap에서 찾아서 결과로 리턴할 배열의 값에 밀어넣었다.

#### Space complexity
- HashMap에 put 하기 때문에 최대 주어진 배열 B 길이만큼 공간을 사용(O(n))

#### Time complexity
for loop을 두번 돌아 2n, 상수 제거하고 O(n)

작성한 코드는 요기에: [my leetcode repo](https://github.com/dayoungles/leet_code/commit/1e2ea21024fab9afd1357b66292ffd85077db8ad#diff-10c5caed9b2c29315ef1b8dc57be2147)

[References]
[Leet code problems](https://leetcode.com/problems/find-anagram-mappings/)