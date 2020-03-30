---
layout: post
title: Longest Parlinedrome
categories: [Leetcode]
---

지난 주의 문제가 이번 주까지 넘어왔다. 주어진 스트링에서 가장 긴 회문을 찾아서 잘라내어 리턴하는 것이 이 문제의 요구사항이었다. 직접 풀지 못하고 솔루션을 참고함.   

```
예시: 
Input: "babad"
Output: "bab"
Note: "aba" 도 가능
```

오전에 문제풀이를 시작하고 혼자서 어영부영 답을 내지 못한 문제는 이번이 처음이었다. 그냥 답도 베껴보았다. 이거 easy라더니 누가 easy래...나의 자신감을 깎아먹어버림.
 

```java
    int low, maxlen;
        public String longestPalindrome(String s) {
            int len = s.length();
    
            if(len<2) {
                return s;
            }
    
            for (int i = 0; i < len - 1; i++) {
                extendIdx(s, i, i);
                extendIdx(s, i, i + 1);
            }
            return s.substring(low, low+maxlen);
    
        }
    
        private void extendIdx(String s, int j, int k) {
            while(j >= 0 && k< s.length() && s.charAt(j) == s.charAt(k)) {
                j--;
                k++;
            }
            if(maxlen < k-j-1) {
                low = j +1;
                maxlen = k - j - 1;
            }
        }            
```

두번째 테스트 같은 경우에는 좀 의아할  수 있는데, 코드 상에서 주석을 보더라도 예상할 수 없다. 원래 while문을 돌 때 같을 떄 조건도 안에 함께 포함되어 있었고 즉 A를 세번 반복했을 떄 B는 substring이 아니라서 -1을 리턴해버리는 문제가 있었다. 그걸 해결하려고 주석 내부의 for문을 추가한건데, 결국 다른 사람의 솔루션을 확인하니 딱 두번만 더 확인하면 되니 if두개로 확인하는 것을 보고 나쁘지 않다는 생각이 들어서 추가했다. 내용은 결국 같다. 

**[References]**

[Leet code problems](https://leetcode.com/problems/longest-parlindrome-string/)


**Space complexity**
O(n): B만큼의 혹은 약간 더 긴 StringBuilder(builder가 속도가 빠르더라) 

**Time complexity**
O(n): B만큼의 길이를 while문을 돌아야 하니 O(B/A)
---

**[Source code]**

[github repo](https://github.com/dayoungles/leet_code/commit/967e28e680c9104e0465a040ddfb0abed578e9cb)
