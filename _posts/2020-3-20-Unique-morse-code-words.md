---
layout: post
title: Unique Morse Code Words
categories: [Leetcode]
---

오늘의 릿콛 문제 풀이는 주어진 String array에 있는 String을 몰스 부호로 바꿔서 concatenation할 때 같은 결과가 있는지 확인하는 것이었다.  

책에서 읽던 모스 부호가 Morse code라고 쓰는 것을 오늘 배웠다. 오 모스 부호! 라고 문제를 읽고 잠시 후에 반가워했다. 물론 반가워 할 이유도 없다. 몰 부호 SOS도 모른다. 아는 것이라서 반가웠나? 한번에 방향을 잡았고 문제를 푸는데는 10분 정도 걸렸다. 최초에 시간을 좀 썼던 이유는 Character에서 'a'를 뺀 것으로 주어진 몰스 부호의 인덱스를 잡으려고 했는데 string.indexOf(0) 을 하면 첫번째 캐릭터가 나올 줄 알았는데 아니었다. charAt을 써야 하는데 너무 확신을 가지고 찍어보다보니 시간이 오래 걸렸다. 

몰스 부호로 변환하는대로 HashSet에 집어넣고 나중에 해시셋의 사이즈를 리턴했다. 역시나 메모리는 꼴등에 가깝게 잡아먹었지만 속도는 1등!  


```java 
public int uniqueMorseRepresentations(String[] words) {
        String[] morseTable = {".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."};
        char startIndex = 'a';
        Set<String> morseSet = new HashSet<>();

        for (String word: words) {
            StringBuffer sb = new StringBuffer();

            for (char alphabet : word.toCharArray()) {
                sb.append(morseTable[alphabet - startIndex]);
            }
            String morseConverted = sb.toString();
            morseSet.add(morseConverted);
        }
        return morseSet.size();
    }
```

#### Space complexity
words 가 모두 다른 몰스 코드 결과로 리턴될 수 있으니 O(n)

#### Time complexity
O(n*l). n은 words의 개수. l은 각 단어의 길이.

[Source code]
[github repo](https://github.com/dayoungles/leet_code/commit/dc6eabd7cd8603e4c70f9b168eed841169190c5a)
[References]
[Leet code problems](https://leetcode.com/problems/unique-morse-code-words/)