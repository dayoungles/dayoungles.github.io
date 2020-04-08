---
layout: post
title: Rotting Oranges
categories: [Leetcode]
---

풀어내는데 1주일 정도 걸린 문제다. 풀다가 지쳐서 포스팅을 미뤘던지라 뒤늦게 포스팅을 하게 되었다. 자세한 문제 내용은 리트코드에서 참조하면 좋겠다. 기억을 위해 간단히 설명하자면 2*2 배열에 0(빈칸), 1(신선한 오렌지), 2(썩은 오렌지ㅠㅠ)를 넣어서 표기하고 1분이 지날 때마다 썩은 오렌지의 상하좌우에 위치한 신선한 오렌지가 썩은 오렌지로 변하는 것이고 배열 안에 있는 오렌지가 모두 썩은 오렌지가 되는데 걸리는 시간을 리턴하거나, 만약 시간이 지나도 썩지 않는 위치에 오렌지가 남아있을 경우 -1 을 리턴하는 것이다.   



**[References]**

[Leet code problems](https://leetcode.com/problems/rotting-oranges/)

![](/images/resource/OrangesRotten.png)
 

처음 문제를 봤을 때 내부에 오렌지의 위치, 썩음 여부, 썩은 시점을 기록하는 이너 클래스를 만들려고 했다. 작업 도중 그렇게 만들어도 도대체 몇번의 포문을 돌아야 할지, 더 나은 방법이 없을지 고민하게 됐다. 이렇게 무식하게 할리가 없다! 라고 확신을 가지고 다른 방법을 찾는데 이틀 정도 썼고...답답해져서 답을 봤는데 이해가 잘 되지 않아서 시간을 더 썼고, 다음날은 그냥 베꼈는데 에러가 발생해서 뻗었고, 마지막날은 두가지 방법으로 문제풀이를 만들었다. 오늘은 이너클래스 방식으로 정보를 관리하는 방법, 배열 내에 썩은 시점을 숫자로 기록해서 처리하는 방법(답 봄), 큐를 사용하는 방법 총 세 가지를 모두 다 기록해보려고 했는데, 지금보니 이너클래스 버전 소스가 없당...빡쳐서 밀어버렸나봉가...빡치기 전에 답을 한번 봤으면 괜찮았을텐데..아쉽


2. 배열 내에 숫자로 썩은 시점을 기록하는 방법
아래 코드에서 보면 결국 삼중포문을 돌아버린다. 삼중 포문 전에 있는 첫번째 이중 포문에서는 주어진 배열 두개를 돌면서 신선한 오렌지인지 여부를 확인한다. 그 다음에는 Fresh Orange numbers 를 가장 외부의 포문에서 체크하고 round(걸린 시간)을 추가한다. 동작은 하지만 For문의 조건에 이렇게 많은 정보를 넣는게 가독성에 좋지 않다고 생각한다. while로 잘 처리할 수 있지 않았을까. 내부의 이중 포문은 다시 주어진 배열을 돌면서 썩은 오렌지를 발견하면 rot 메서드에 보내서 상하좌우를 확인하는데 문제를 단순화 한다는 관점에서 좋게 생각했다. 내가 작성할 때는 저 위치에 if문을 각각 걸어서 배열의 인덱스를 넘어서진 않는지 확인해야 했기 때문이다. 

rot 은 그런 점에서 or 조건 한방으로 인덱스의 길이를 넘어서진 않는지? 혹은 -1위치를 가리키지는 않는지? 등을 모두 확인해버려서 좀 더 깔끔해지긴 한다.   
  
```java
    public int orangesRotting(int[][] grid) {
        int round = 0;
        int fresh = 0;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                if(grid[i][j] == 1)
                    fresh++;
            }
        }

        for(int oldFresh= fresh; oldFresh>0; round++, oldFresh=fresh){
            for(int i = 0; i< grid.length; i++){
                for(int j = 0; j< grid[i].length; j++){
                    if(grid[i][j] == round+2) {
                        fresh -= rot(grid, i+1, j, round) +
                                rot(grid, i-1, j, round) +
                                rot(grid, i, j+1, round) +
                                rot(grid, i, j-1, round);

                    }
                }
            }
            if(fresh == oldFresh) return -1;
        }
        return round;
    }
    
    private int rot(int[][] grid, int i, int j, int day) {
        if(i<0 || j<0 || i>=grid.length || j>=grid[i].length || grid[i][j] != 1)
            return 0;
        grid[i][j] = day + 3;
        return 1;
    }
```

**Space complexity**

O(n): 원래 배열만 사용 

**Time complexity**

O(n^3): 삼중포문..맞는거지? 전체 배열이 모두 다 신선한 오렌지일 수 있기 때문에 최악의 경우에는 삼중 포문을 아주 꽉꽉(꽉꽉 이래도 아마 n보다 작은 상수겠지만 )돌아야 할 수도 있다는 것.


3. Queue를 활용한 것
마찬가지로 첫번째 포문은 전체 배열을 순회하면서 썩은 오렌지가 있으면 썩은 오렌지의 위치와 썩은 시점을 Pair객체로 집어넣는 것이다. 그리고 while문을 돌면서(도는 횟수를 ++시켜서 최종 값이 다 썩는데 걸린 시간) 썩은 오렌지가 빌 때까지 queue를 비운다. 그리고 그 썩은 오렌지의 상하좌우에 신선오렌지가 있는지 확인하고, 있다면 그 오렌지도 썩은 오렌지로 표기해서 큐에 넣는다. 큐가 다 비었는데 아직 안 썩은 오렌지의 개수가 남아있다면? -1을 리턴하면 된다.  

```java
public int orangesRottingWithQueue(int[][] grid) {
        Queue<Pair<int[], Integer>> q = new LinkedList<>();
        int fresh = 0;
        int round = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
                int orange = grid[i][j];
                if(orange == 2) {
                    q.add(new Pair(new int[] {i, j}, 0));
                }
                if (orange == 1) {
                    fresh++;
                }
            }
        }

        while(!q.isEmpty()) {
            Pair<int[], Integer> p = q.poll();
            int row = p.getKey()[0];
            int col = p.getKey()[1];
            int rottenRound = p.getValue();

            round = rottenRound;
            //upper i-1, j
            if(row -1 >= 0 && grid[row-1][col] == 1) {
                grid[row-1][col] = 2;
                fresh--;
                q.add(new Pair (new int [] {row - 1, col}, rottenRound +1));
            }
            //below i+1, j
            if(row +1 < grid.length && grid[row+1][col] == 1) {
                grid[row+1][col] = 2;
                fresh--;
                q.add(new Pair(new int[] {row + 1, col}, rottenRound +1));
            }
            //left i, j-1
            if(col -1 >= 0 && grid[row][col-1] == 1) {
                grid[row][col-1] = 2;
                fresh--;
                q.add(new Pair(new int[] {row, col - 1}, rottenRound +1));
            }
            //right i, j+1
            if(col +1 < grid[row].length && grid[row][col+1] == 1) {
                grid[row][col +1] = 2;
                fresh--;
                q.add(new Pair(new int[]{row, col + 1}, rottenRound+1));
            }
        }
        return (fresh > 0) ? -1:round;
    }
``` 

**Space complexity**

O(n): 썩은 오렌지 개수만큼 큐를 사용한다네 


**Time complexity**

O(n): 썩은 오렌지 하나가 들어갈 때마다 다른 오렌지들이 또 들어간다네.

---

**[Source code]**

[github repo](https://github.com/dayoungles/leet_code/commit/e534c94cdf70632680e42c016791a4f550dc7e08)
