---
title: "DP (Dinamic Programming) 알고리즘"
date: 2018-10-05 10:32:00 -0400
categories: python
tags: Algorithm
---

> 출처: Seul Lee(이슬)님 사이트를 참고하였습니다 => [DP 관련1](https://lee-seul.github.io/algorithm/2017/03/16/dynamic-programming.html) <br>
출처: c0smicb0y님 사이트를 참고하였습니다 => [DP 관련2](http://janghw.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Dynamic-Programming-%EB%8F%99%EC%A0%81-%EA%B3%84%ED%9A%8D%EB%B2%95)

## <span style="color:#36999F"> Dynamic Programming(DP, 동적계획법) </span>
- <mark> 큰 문제를 작은 문제로 나눠서 푸는 알고리즘 </mark>
- 분할 정복법, 점화식과 유사
- 공간복잡도를 늘리고, 시간복잡도를 줄이는 방식

## <span style="color:#36999F"> DP 사용 조건 </span>
- Overlapping subproblem : <br> 겹치는 부분 문제, 즉 같은 값을 여러번 구하는 것을 의미
- Optimal substructure : <br> 전체 문제의 답이 부분 문제의 답으로부터 만들어지는 구조
    - 대표적인 예: 피보나치 수열

## <span style="color:#36999F"> DP 사용 예시 </span>
1. dp 배열 : 각 정사각형의 최대 넓이를 저장할 dp 배열 생성
2. 정답 변수 선언
3. 주어진 배열의 가로 길이와 세로 길이 값을 구한다.
4. 주어진 배열의 각 칸을 하나씩 순회하기 위해서 이중포문을 작성한다.
    - (0,0)부터 시작하면 배열의 인덱스를 넘는 문제가 발생할 수 있으므로, dp 배열의 (1,1) 인덱스부터 시작하게 하고,
    - 그 외에 범위를 벗어난 값을 읽으려고 할 때는 항상 0을 구할 수 있게 간단한 처리를 할 수 있다. <br>
        -> <mark> if(board[i-1][j-1] != 0 ) </mark>
5. dp 사용: dp[i][j] = min(dp[i][j-1], <mark> min(dp[i-1][j], dp[i-1][j-1])) + 1 </mark>,
    answer를 매번 갱신을 해주면 된다.
    
         
```python
#include<vector>
using namespace std;


int dp[1001][1001] = {0};

int solution(vector<vector<int>> board)
{
    int ans = 0;
    int row = board.size();
    int col = board[0].size();
    for (int i = 1; i <= row; ++i)
    {
        for (int j = 1; j <= col; ++j)
        {
            if(board[i-1][j-1] != 0 )
            {
                dp[i][j] = min(dp[i][j-1], min(dp[i-1][j], dp[i-1][j-1])) + 1;
                ans = max(ans, dp[i][j]);
            }
        }
    }
    return ans*ans;
}
```