---
title: Leetcode: Subrectangle Queries
author: Dayoungle
date: 2021-09-15 08:00:00 +0900
categories: [Leetcode,medium]
tags: [Leetcode]
---

## Add Two Numbers

여기 블로그 어디인가를 살펴보면, 아마 이 문제를 풀었던 기록이 있을 것이다..몇번이나 풀었던 문제니까.
ListNode는 아래와 같이 생겼다.
```Java
public class ListNode {
     int val;
     ListNode next;
     ListNode() {}
     ListNode(int val) { this.val = val; }
     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```

풀이는 간단하다. 대신 어떻게 ListNode를 적게 정의해서 메모리를 어떻게 적게 쓸 것인지에 대한 고민을 하게 된다. 로직을 구현하고 나서 메모리를 줄이려고 생각하게 되면 로직이 바뀌는 필연적인 결과에 도달한다. 내 경우, 메모리를 남용하기로 결정하고 두개의 head node를 추가로 정의했는데, 결국 돌아보니 필요가 없더라. 날려버렸다.

```Java

```


[Reference]
- [Leet code: Add Two Numbers](https://leetcode.com/problems/add-two-numbers)
- [Github](https://github.com/dayoungles/leet_code/blob/master/src/leet/AddTwoNumbers.java)
