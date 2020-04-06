---
layout: post
title: Add String
categories: [Leetcode]
---

이건 오늘 푼 문제로 소소하게 버그를 많이 잡아야 했다. String으로 주어진 숫자를 더해서 다시 스트링으로 return 하라고 했다. 처음엔 예외조건을 유심히 보지 않고 "뭐여...?" 하고 Integer.parseInt와 String.valueOf를 이용해서 한줄로 돌렸다. 그리고 제출했더니 에러가 팡! 이유는, 하나의 스트링이 최대 5000개까지 숫자를 가질 수 있기 때문이었다. 아하하 역시 그렇게 쉬운 문제가...하고 다시 풀어냄. 스트링을 1의 자리부터 하나씩 쪼개서 더해서 올림값을 올려주는 방식을 취하고 더한 결과 값은 StringBuffer에 집어넣은 후, 모든 작업이 완료되면 StringBuffer를 reverse 시켰다.   


**[References]**

[Leet code problems](https://leetcode.com/problems/add-strings/)

```
예시: 
Input1: "10020"
Input2: "23"
Output: "10043"
```
 

```java
    int len1 = num1.length();
    int len2 = num2.length();
    int idx1 = 0, idx2 = 0;
    int ollim = 0;
    StringBuffer sb = new StringBuffer();

    while (len1 > idx1 || len2 > idx2 || ollim > 0) {
        int val1 = 0;
        int val2 = 0;

        if(idx1 < len1) {
            val1 = Integer.parseInt(String.valueOf(num1.charAt(len1-1-idx1)));
        }

        if(idx2 < len2) {
            val2 = Integer.parseInt(String.valueOf(num2.charAt(len2-1-idx2)));
        }

        int sum = val1+val2 + ollim;
        ollim = 0;

        if (sum >= 10) {
            ollim = sum / 10;
            sum = sum % 10;
        }
        sb.append(sum);
        ++idx1;
        ++idx2;
    }

    return sb.reverse().toStr'ing(); 
```

첫 번째 버그는 올림 이라고 써둔, 말그대로 10을 넘은 올림 값을 어디에서도 초기화 하지 않아서 한번 올림값이 갱신되면 계속 그 올림값이 살아있는 문제가 발생했다. 올림값은 sum에 값을 더해준 후에 바로 초기화 하는 것으로 해결했다. 

두 번째 버그는 올림을 초기화 하고 나서 따라오는 if 문에 sum값을 넣는게 아니라 value값 두개를 더하기만 했다는 것. 올림이 당연히 제대로 되지 않아서 그것도 fix. 

전체적으로 헤맸던 것이 처음 생각했던 방향은 index를 사용하는 것이 아니라 각 문자열의 길이를 하나씩 줄여나가면서 while진입 조건으로 사용하려고 했었다. 당연히 index가 필요해졌고, index를 사용하고 나니 굳이 len을 선언해야 할 필요가 있었나 싶다. 

그리고 while문의 진입 조건으로 올림값이 0이 아닐  때를 집어넣는 것도 중요했다. 왜냐하면 처음 계획은 while문의 조건이 이러했기 때문.  

```java
while(len1 +1 >= idx1 || len2 +1 >= idx2) {...}
``` 
즉, 올림이 발생할 수도 있다는 가정을 항상 고려해서 한칸을 더 계산하는 작업을 하는 것이었고 따라서 실제 올림의 발생 여부와 관계없이 0이 하나 더 붙어야 하는 상황이었다. 이걸 개선해 줄 수 있었던 것이 각 숫자의 인덱스를 넘어서는 상황이 오더라도 올림값이 있으면 그 올림값을 덧붙여줄 수 있도록 지금의 while 조건을 추가하는 것이었다. 그리고 +1 을 더하는 상황도 불필요해졌다. 지난주에 너무 고생스러워서 쉽게 풀었더니 행복하다.  

**[References]**

[Leet code problems](https://leetcode.com/problems/add-strings/)


**Space complexity**
O((num1.length \|\| num2.length)+1) 가장 긴 스트링에서 올림을 추가하게 되면 + 1 


**Time complexity**

O((num1.length \|\| num2.length)+1)

---

**[Source code]**

[github repo](https://github.com/dayoungles/leet_code/commit/cb948dce42967f719c8ca99d3cf7de30bc7efdfe)
