---
layout: post
title: Single row keyboard 
categories: [Leetcode]
---

오늘의 문제는 두개의 문자열-26자리의 순서가 없는 알파벳 세트 하나와 특정한 단어-을 주고 두번째 단어를 알파벳 세트에서 인덱스로 가리키기 위해서 몇 번을 인덱스가 옮겨다녀야 하느냐 하는 것이었다. 

답도 줬다. \|i - j \| 가 답이라고...ㅎㅎ오래 고민하지 않았고, 실수가 있었다면 목표지점까지 도착했을 때 인덱스를 교체해주지 않은 점. 


```java 
public int calculateTime(String keyboard, String word) {
        int idx = 0;
        int count = 0;
        for (char alphabet: word.toCharArray()) {
            int newIdx = keyboard.indexOf(alphabet);
            count += Math.abs(newIdx - idx);
            idx = newIdx;
        }
        return count;
    }
```

#### Space complexity
O(1) 인덱스, 카운트 개수 만큼

#### Time complexity
**O(n\*m)**

word의 자리수 만큼 O(word.length) 키보드의 indexOf를 할 떄 주어진 키보드 스트링 길이만큼 순회해야 하니 O(keyboard.length)



[Source code]
[github repo](https://github.com/dayoungles/leet_code/commit/0481f02bb29e9b5b7811586ac7751cdd456a2c46)
[References]
[Leet code problems](https://leetcode.com/problems/single-row-keyboard/)
