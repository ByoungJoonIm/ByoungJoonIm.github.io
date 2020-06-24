---
layout: post
title:  "[알고리즘 분석] DFS(Depth First Search) 응용"
date:   2020-06-24 15:54:00
categories: Algorithm
tags: algorithm java concept analysis
---

## 개요
- RxC의 2차원에서 길을 찾거나, 경우의 수를 탐색하는 경우에 DFS를 유용하게 사용할 수 있다. 특히 경우의 수를 탐색하는 경우에 많이 사용되는데, 이때 어떻게 재귀를 제어하는지 살펴보자. 
- DFS의 depth를 제어하는 방법을 '백트래킹' 이라고 부른다.
- [백준 N과 M 시리즈](https://www.acmicpc.net/workbook/view/2052)를 풀어보며 어떻게 접근하는지 알아본다.

## 어떨때 사용하면 좋을까?
- 반복문이 n번 중첩될 때 사용하면 유용하다.

### N과 M시리즈 1번(15649번)
## 생각 포인트
- '중복 없이'라는 키워드를 본다면, 다음과 같은 키워드를 떠올려야 한다.
  - HashSet
  - visited (이미 방문한 곳은 다시 방문하지 않는 것의 의미에서)
    - 이 문제에서는 visited를 사용했지만, hashSet을 사용해도 무방하다.
- '사전순'이라는 키워드를 본다면, 다음과 같은 해석을 생각해 볼 수 있다.
  - 우리가 출력하고자 하는 배열은 오름차순으로 정렬되어 있어야 한다.
  - 단, 이 문제에서는 이미 정렬된 배열이나 다름없다.(1,2,3 순으로 증가하므로)
- 반복문의 중첩이 얼마나 일어나야 할까?
  - 만약 이 문제가 완전탐색 문제라고 생각해보자. M의 범위가 1~8이므로 최대 8번의 반복문 중첩이 일어나야 한다.
  - 중첩을 코드로 작성하는게 가능할까?(8중 for문)
- 이 문제는 순열 문제일까 조합 문제일까?
  - 예제를 보면 `1 2`와 `2 1`은 다른 결과를 보이는 것을 볼 수 있다.
  - 따라서 이 문제는 순열을 물어보는 문제이다.
  
## 코드
```java
package forRank;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.StringTokenizer;

public class Q15649 {
	private static int N, M;
	private static StringBuilder sb;
	private static int selected[];
	
	private static void dfs(int depth, boolean visited[]){  //depth는 몇번째 중첩된 for문인지를 나타냄
		if(depth == M){               //중첩된 for문중 가장 안쪽에서 벌어질 일
			for (int i = 0; i < M - 1; i++)
				sb.append(selected[i]).append(' ');
			sb.append(selected[M - 1]).append('\n');
			return;
		}
		
		for (int i = 0; i < N; i++) { //중첩될 for문
			if(!visited[i]){
				selected[depth] = i + 1;
				visited[i] = true;
				dfs(depth + 1, visited);
				visited[i] = false;	
			}
		}
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		sb = new StringBuilder();
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		
		selected = new int[M];
		
		dfs(0, new boolean[N]);
		
		bw.write(sb.toString());
		
		br.close();
		bw.close();
	}
}

```

### 코드 해석
- N개중 M개를 사전 순서로 골라야 하므로, M개의 중첩 for문이 필요하다. dfs라는 함수로 중첩 for문을 구현하였다. 
- M번의 for문 중첩이 일어난 뒤에는 비로소 M개의 숫자를 모두 고를 수 있으므로, 출력한다.
- visited를 true/false로 제어하는 것은 어떤 의미일까? 예를 들어 N은 3이고, M은 2일때 visited가 어떻게 변화하는지 관찰해 보자.

```java
package test;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class VisitedTest {
	private static int M, N;
	private static StringBuilder sb;
	
	private static void dfs(int depth, boolean visited[]){
		if(depth == M){
			for(int i = 0; i < N - 1; i++)
				sb.append(visited[i]).append(' ');
			sb.append(visited[N - 1]).append('\n');
			return;
		}
		
		for (int i = 0; i < N; i++) {
			if(!visited[i]){
				visited[i] = true;
				dfs(depth + 1, visited);
				visited[i] = false;
			}
		}
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		sb = new StringBuilder();
		
		N = 3;
		M = 2;
		
		dfs(0, new boolean[N]);
		
		bw.write(sb.toString());
		
		br.close();
		bw.close();
	}
}

```

```
//결과
true true false  -> 1, 2를 선택
true false true  -> 1, 3을 선택
true true false  -> 2, 1을 선택
false true true  -> 2, 3을 선택
true false true  -> 3, 1을 선택
false true true  -> 3, 2를 선택
```

- 즉, N개중 M개를 선택하는 경우에 visited는 유용하게 사용될 수 있다.
