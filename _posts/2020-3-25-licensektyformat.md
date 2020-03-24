---
layout: post
title: License Key Format
categories: [Leetcode]
---

오늘의 문제는 주어진 String license를 두번째 인자로 주어진 숫자 크기에 맞춰 '-' 대쉬를 입력하고, 또 전체를 대문자로 바꾸는 문제였다. 단 수트링의 길이가 만약 주어진 숫자의 배수가 아닐 경우, 나머지(K보다 짧은 스트링)는 앞에 배치한다. 설명이 힘드네...아래 샘플이 있다.

```java
Input: S = "2-5g-3-J", K = 2
Output: "2-5G-3J"
```

[Leet code problem link] (https://leetcode.com/problems/license-key-formatting/)

 
처음에는 Stack에 쌓아넣고 하나씩 뽑아내는 방식을 생각했다. 그런데 숫자의 크기만큼 대시를 집어넣는 방식이 뒤에서부터 진행돼야 한다는 것을 깨달았다. 그래서 스택을 포기하고 스트링버퍼를 뒤집는걸 생각했다. 틀렸던 테스트 케이스가 나왔는데 알파벳은 없이 "------"라고 나온 것들. 그걸 해결 하기 위해서는 소스의 위치를 변경할 필요가 있었는데, 대쉬 기호를 어느 시점에 붙여주느냐의 문제. 나는 일단 주어진 숫자의 크기를 다 채우면 무조건 앞에 대쉬를 붙여줬다. 즉 아래 소스의 두 번째 if문이 원래 for loop의 가장 마지막에 있었던 것. 그래서 처음 소스에서는 마지막에 다 돌고 나서 리턴 값 앞에 대쉬기호가 있는지 확인하고 지우는(sb 인덱스 삭제할 때 array copy한다..ㅂㄷ) 작업을 따로 했는데, 다 완료 하고 나서 솔루션을 보니 카운트를 앞으로 내보내고 카운트를 뒤에 ++시키는 방법도 있었다. 즉 다음 번 포문을 돌 때 붙여야 할 차례인지를 확인하는 것. 똑같은 코드를 훨씬 줄일 수 있었다. 

```java 
    public String licenseKeyFormatting(String S, int K) {
            StringBuffer sb = new StringBuffer();
            int count = 0;
            for (int i = S.length()-1; i >=0; i--) {
                if (S.charAt(i) == '-'){
                    continue;
                }

                if (count == K) {
                    count = 0;
                    sb.append('-');
                }

                sb.append(Character.toUpperCase(S.charAt(i)));
                count++;
            }
    
            return sb.reverse().toString();
    
        }
```


**Space complexity**

O(n): string에 만약 주어진 내용이 모두 알파벳이라면 O(n + n/k) == O(n) 

**Time complexity**

O(n). StringBuffer reverse 도 bit 연산으로 한번에 옆으로 쭉 땡기는 듯. 다행이다.  

-----

**[Source code]**

[github repo](https://github.com/dayoungles/leet_code/commit/4566e45655068ba59b679abfaf2292038117043a)

**[References]**

[Leet code problems](https://leetcode.com/problems/license-key-formatting)