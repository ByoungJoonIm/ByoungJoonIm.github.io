---
layout: post
title:  "[알고리즘 분석] 이진 탐색(binary search)"
date:   2020-01-25 23:13:00
categories: Algorithm
tags: algorithm java concept analysis
---

## 개요
- 이진 탐색을 사용하다보면, 인덱스에 대해서 생각해볼 필요가 있음을 느낀다. 특히 기본적인 탐색 이외에 응용할 방법이 많기 때문에, 인덱스에 대해 한번 정리하고자 한다.

## 기본 개념
- 이진 탐색은 정렬된 배열이 있을 때, O(logn)의 시간에 탐색할 수 있는 방법이다.
- 이진 탐색을 수행할 때, 다음과 같은 특징을 가진다.
  - 배열의 원소의 수는 상관이 없다.
  - 원소의 수가 짝수나 홀수인 경우 모두 동일하게 작동한다.
  
## 기본 방법
- arr : 정렬된 배열
- L : 왼쪽 인덱스
- R : 오른쪽 인덱스
- M : 중앙 인덱스( M = (L + R) / 2 )
- 탐색값 : 탐색하고자 하는 값

## 심화 개념
- 이진 탐색이 성공한 경우와, 실패한 경우 인덱스가 어떻게 변화되는지 관찰해볼 필요가 있다.
  - 이진 탐색이 성공한 경우
    - 탐색 값 == arr[M]
  - 이진 탐색이 실패한 경우
    - 탐색값 > arr[0]일 때, arr[R]은 탐색값보다 작은 값 중 최대값이다.
    - 탐색값 < arr[0]일 때, R은 -1이다.
    - L <= R 조건에 걸리지 않는 경우(L > R) M의 값은 재계산 되지 않는다. 즉, M은 일정한 규칙을 가지지 않는다.

## 경우 따져보기
![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2020-01-25-analysis-001.jpg?raw=true)

## 이 개념을 활용하여 풀어볼만한 문제
- [백준 2805, 나무자르기](https://www.acmicpc.net/problem/2805)

## 이 개념을 활용한 소스코드 예제(풀이의 정답)
```java
package forRank;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.StringTokenizer;

public class Q2805 {
	private static final int TREE_HEIGHT_MAX = 1000000000;
	private static int N;	//나무 수
	private static int M;	//집에 가져가려는 나무의 길이
	private static int trees[];
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

		//inputs
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		trees = new int[N];
		
		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++)
			trees[i] = Integer.parseInt(st.nextToken());
		
		//algorithm
		int low = 0;					//L
		int high = TREE_HEIGHT_MAX;		//R
		int mid = 0;					//M
		
		//이 문제에서는 (탐색값 < arr[0])인 경우를 고려하지 않아도, 데이터 자체가 조건을 만족하게 주어짐
		while(low <= high){
			mid = (low + high) / 2;
			long sum = 0;
			
			for (int i = 0; i < N; i++)
				sum += ((trees[i] <= mid) ? 0: trees[i] - mid);
			
			if(sum == M){			//이진 탐색이 성공한 경우. 이 이외 경우는 모두 탐색 실패
				high = mid;			//탐색 실패시 high(R)를 사용하므로, 결과를 high에 저장
				break;
			} else if(sum > M){
				low = mid + 1;
			} else {
				high = mid - 1;
			}
		}
		
		bw.write(high + "\n");		//결과로 R번째 인덱스 출력. 이 문제에서는 인덱스를 바로 출력
		
		br.close();
		bw.close();
	}
}

```
