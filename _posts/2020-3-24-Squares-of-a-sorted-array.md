---
layout: post
title: Squares of a sorted Array 
categories: [Leetcode]
---

오늘의 문제는 sorted된 array(including negative)의 square 값들을 sorted array로 다시 만들어서 내보내는 것이었다.   
 
### Challenge 1 
for loop list에 제곱해서 집어넣은 다음에 리스트 자체를 Collections.sort로 해결. 다시 int array로 돌리기 위해 for loop 를 다시 돌았음. 직관적으로 생각이 들었고 동작하는거 본 다음에 linked list로 포문을 한번만 돌면서 할 수 있을거라고 생각함. submit 성공. 

```java 
    public int[] sortedSquares_easy(int[] A) {
        List<Integer> list = new ArrayList<>();

        for (int i:A) {
            list.add(i*i);
        }

        Collections.sort(list);

        int[] result = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            result[i] = list.get(i);
        }
        return result;
    }
```


**Space complexity**

O(n): A.length 만큼 *2번새로운 배열을 선언 

**Time complexity**

Collections.sort 만큼의 시간 복잡도가 될 것. 


### Challenge 2
샘플 문제는 동작하는데 time limit에 걸려서 submit을 받아주지 않음. 1번 답을 생각하면서도 어렴풋이 링크드 리스트로 해결할수 있을거라고 생각했던 것은 linkedlist를 한번만 돌면서 중간에 끼워넣을 수 있으니까 성능이 더 좋을거라고 생각했는데, 짜다보니 double for loop 를 만들어버린 것이어따...중간에 반성했지만 일단 돌아가는지 보고 싶어서 실행. 10000개짜리 테스트 케이스에서 깨졌다.  

```java
    public int[] sortedSquares_linkedlist(int[] A) {
        LinkedList<Integer> list = new LinkedList<>();

        for (int i:A) {
            int current = 0;
            int idx = 0;

            for(int j = 0; j < list.size(); j++) {
                current = list.get(j);
                if (current >= i * i) {
                    break;
                }
                idx++;
            }
            list.add(idx, i*i);
        }

        int[] result = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            result[i] = list.get(i);
        }
        return result;
    }
```


**Space complexity**

O(n): A.length 만큼 *2번새로운 배열, 링크드 어레이 선언 

**Time complexity**

O(n^2)



### Solution 참고
더 나은 생각이 들지 않아서 솔루션을 봤는데, 내가 무심히 놓친 부분이 시작할 때 주어지는 array가 이미 sorted라는 것이다. 이미 정렬되어 있다는 부분에서 얻을 수 있는 것..양쪽 끝이 가장 클 가능성이 높은 두 수라는 것. 이걸 고려하지 않았기 때문에 더 새로운 아이디어가 나올 수 없었다. 문제를 잘 읽자. 

양쪽의 index를 각각 head, tail 로 놓고 while문을 돌면서 제곱승을 해서 더 큰 숫자를 사전에 선언해둔 배열의 끝부터 채워넣는다. 처음에 실패했었는데, 그 이유는 tail도 ++시켜서 신나게 Array outof index 가 떨어졌고 디버깅하다보니 tail놈이 ++되고 계셔서 고침. 두번째도 에러가 났는데 두번째에는 answeridx를 옮겨주지 않고 제일 끝 자리만 계속 갱신하고 있어서 고침. 
 
```java
    public int[] sortedSquares_solutionWithMergeSort(int[] A) {
        int head = 0;
        int tail = A.length-1;
        int[] answer = new int[A.length];
        int answerIdx = A.length-1;

        while(head <= tail) {
            int headSquared = A[head]*A[head];
            int tailSquared = A[tail]*A[tail];

            if(headSquared >= tailSquared) {
                answer[answerIdx] = headSquared;
                head++;
            } else {
                answer[answerIdx] = tailSquared;
                tail--;
            }
            answerIdx--;
        }
        return answer;
    }
```


**Space complexity**
O(n) : return 하는 새로운 배열 크기 

**Time complexity**
O(n) : A의 길이만큼 한번 실행 
word의 자리수 만큼 O(word.length) 키보드의 indexOf를 할 떄 주어진 키보드 스트링 길이만큼 순회해야 하니 O(keyboard.length)

-----

**[Source code]**

[github repo](https://github.com/dayoungles/leet_code/commit/18926050e310edbbf3c55340ddb28428d9973cb3)

**[References]**

[Leet code problems](https://leetcode.com/problems/squares-of-a-sorted-array/)