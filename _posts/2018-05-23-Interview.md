---
layout: post
title:  "[Interview] Interview 준비"
date:   2018-05-23 17:22:00 +0900
categories: Network
tags: [Network, IP, TCP]

---

## Interview 준비
---


![Interview](http://farm3.static.flickr.com/2819/9516543726_6da0beed18_z.jpg)

면접이 얼마 남지 않았다.

내가 했던 프로젝트들, 기본 CS를 정리하고 면접전에 한번에 보기 위해 정리해 두기로 했다.

SW회사에서 면접을 몇번 진행했다보니, 그 특징을 조금씩 이해해왔는데, 사실 직접적으로 정의를 묻지는 않는다. (SI 회사나 제조분야와 같이 직접적인 SW개발을 하는 회사가 아니라면 묻는 경우도 많은 듯 하다)

다만, 자신이 했던 프로젝트에 해당 내용을 물을 필요가 있다면 응용하여 묻는 편이다.

DB에 정규화 진행을 설명해보라 와 같은 질문이다.

즉, 해당 질문에 대해 대답하려면 정의를 알고 그에 필수적인 단어를 언급하며 유사한 답변으로 끌어나가야 한다고 생각한다.

혹은 자신의 경험을 토대로 예시를 이용해 설명하는 것도 차선책이자, 좋은 답변이 된다고 생각한다.

**이번엔 꼭 합격하자.**

먼저 DB 부터 시작하도록 하겠다.

---

### DataBase

---

DataBase를 나는 MySQL을 가장 많이 사용했다.

또한, 포트폴리오를 보면, Oracle 이나, postgreSQL을 사용해 본적도 있다.

그렇다면 이에 대해 비교하는 질문이 예상된다.

이를 한번 정리하고 넘어가보려고 한다.

솔직히 개인 개발을 진행했다보니, 이 차이를 실제 프로젝트에서 느끼기는 힘들었다.

따라서, 이론상으로 정리해 보려 한다.

---

#### DB 간의 차이점

---

이전에 이를 고민하다가 타 사이트를 본 적이 있다.

[출처 : http://d2.naver.com/helloworld/227936](http://d2.naver.com/helloworld/227936)

Naver D2에서 정리한 사항인데, 차이점에 대해서도 정리가 되어 있다.

|   Oracle   | 오랫동안 검증된 방대한 양의 코드, 다양한 레퍼런스. 그러나 비싼 비용이 단점 |
|:----------:|:--------------------------------------------------------------------------:|
| postgreSQL | 오픈소스로 비용 절감, 잘 정돈된 문서, 크게 떨어지지 않는 기능, 신뢰성 우선 |
|    MySQL   |       다양한 응용과 레퍼런스. 그러나 기업형 개발 모델과 라이선스 부담      |

`이런 DB들을 사용해봤다고 하였는데, 어떤 점이 달랐냐`라는 질문이 들어온다면,

아마 나는 개발자체로 느꼈던 것은 크지 않았다. 다만, 이론적으로 대답을 한다면 위와 같다 라고 말해야 할 것이다.

무턱대로 개발해봤다고 이런 점이 다르다라고 한다면, 꼬리물기에 대답못하는 상황이 올 것이다.

모르는 것은 모른다고 하되, 공부를 해봤었는데 여기까지는 안다는 늬앙스가 중요하다.

모든걸 아는 신입은 없다. 다만 내가 이정도는 안다가 중요하다.

---

#### DB 정규화

---

정규화에 대해 한번 정리해 보자.

정규화의 정의는 `데이터 모델을 좀 더 구조화하고 개선시켜 나가는 절차에 관련된 이론`이다.

따라서, 보통 중복이나 종속성을 제거하여 구조를 개선시켜 나간다.

보통 제 3 정규화까지는 잘 알고, 각각을 `도부이결다조`라고 하며, 그 특징을 외우기도 한다.

그 특징의 명명만 알지 제대로 모르는 상황을 막기 위해 하나씩 정리해보려 한다.

[출처 : http://anyjava.tistory.com/33](http://anyjava.tistory.com/33)

---

##### 제 1 정규화

---

**제 1 정규화** 는 `도메인이 원자값`이라는 말로 기억한다.

먼저 **도메인** 이란, `속성에 해당하는 값` 혹은 `속성이 가질 수 있는 값의 범위`를 말한다.

예를 들어, `학생`이라는 테이블에 `성별`이라는 속성이 있을 때, `남자`, `여자` 가 도메인이 된다.

`학점`이라는 속성이 있다면, `0.0~4.5 실수` 가 도메인이 될 것이다.

즉, 1 정규화는 도메인이 원자값이 되어야 한다는 것이다.

중복으로 도메인이 들어간다면, 이를 나누어 주어야 한다.

| 고객번호 | 고객명 |    취미    |
|:--------:|:------:|:----------:|
|     1    | 홍길동 | 운동, 등산 |
|     2    | 김민희 |    노래    |

다음과 같은 테이블을 보면 `취미`라는 `속성`의 도메인이 원자값이 아님을 볼 수 있다.

이를 해결해본다면, 테이블을 2개로 나누어야 한다.


| 고객번호 | 고객명 |
|:--------:|:------:|
|     1    | 홍길동 |
|     2    | 김민희 |

| 고객번호 | 일련번호 | 취미 |
|:--------:|:--------:|:----:|
|     1    |     1    | 운동 |
|     1    |     2    | 등산 |
|     2    |     1    | 노래 |


일련번호는 취미가 여러개이기 때문에 구분하려 만든 속성이다.

---

##### 제 2 정규화

---

**제 2 정규화** 는 흔히, 제 1 정규화를 만족하며, `부분적 함수 종속 제거` 한 것이라고 한다.

`부분적 함수 종속`이 무엇일까?

먼저 `함수 종속`이 뭔지 알아보자.

함수라고 해서 갑자기 왠 함수지 할 수도 있지만, 실상은 간단하다.

`A->B(A이면 B이다) 일때 B는 A의 함수 종속이라 한다.`

예를 들어 주민번호와 이름을 들 수 있다.

A라는 주민번호을 가지고 있다면 B 라는 이름을 가진다라는 것은 항상 참이다.

즉, 이때 `B는 A의 함수 종속`이라 하는 것이다.

`하나의 속성이 다른 속성의 유일함을 결정하는 것`이다.

그리고 제 2 정규화는 우선적으로 다음을 **전제** 한다.

    복합키(Composit Primary Key) 에 전체적으로 의존하지 않는 속성들을 제거한다.

즉, `제 2정규화의 대상이 되는 테이블은 키가 여러 칼럼으로 구성된 경우이다.`

따라서, 제 2 정규화는 **키에 의존적(지배적)** 이다.

하나의 테이블에서 키가 아닌 일반 컬럼(속성)들은 모두 기본키에 의해 지배되어야 한다.

허나 다음 예시를 보자.

| 사번 |  프로젝트  | 부서 |  역할  |
|----------|:------:|:--------:|:------:|
| 1        | ㄱ |     SW개발    | 부팀장 |
| 1        | ㄴ |     SW개발    |  팀장  |
| 2        | ㄴ |     마케팅    |  사원  |
| 3        |  ㄱ  |     제조    |  팀장  |


다음과 같은 테이블이 있다할 때, **기본키** 는 `사번과 프로젝트`이다.

이때, 부서는 사번에 대해서 부분적으로 함수 종속이 된다.

즉, 프로젝트와 상관없이 사번에만 부분적으로 함수 종속이 된다는 것이다.

따라서, 이를 제거해 주어야 한다.

앞선 정의를 따라, 사번(A)이면 부서(B)임을 참으로 한다.

즉, 위와 같은 상황을 해결하면 제 2 정규화를 만족하는 것이다.

따라서, 다음과 같이 테이블이 나누어 진다.

| 사번 | 프로젝트 |  역할  |
|----------|:--------:|:------:|
| 1        |    ㄱ    | 부팀장 |
| 1        |    ㄴ    |  팀장  |
| 2        |    ㄴ    |  사원  |
| 3        |    ㄱ    |  팀장  |

| 사번 |  부서  |
|------|:------:|
| 1    | SW개발 |
| 2    | 마케팅 |
| 3    |  제조  |


[출처 : http://clearpal7.blogspot.kr/2016/07/2_26.html](http://clearpal7.blogspot.kr/2016/07/2_26.html)

---

##### 제 3 정규화

---

**제 3 정규화** 는 제 2 정규화를 만족하며, `이행적 함수 종속 제거` 한 것이라고 한다.

함수 종속은 아는데 `이행적` 함수 종속은 무엇일까?

흔히, `A->B이고 B->C일 때 A->C를 만족하는 관계`라고 말한다.

그러나 좀더 쉽게 설명하자면, `기본키(Primary Key)에 의존하지 않고 일반 컬럼에 의존하는 칼럼들을 제거한다.`라고 생각하면 된다.

예시를 통해 두가지 설명이 어떻게 연결되는 지 보자.


| 사번 | 프로젝트 |  역할  | 고가 |
|:----:|:--------:|:------:|:----:|
|   1  |    ㄱ    | 부팀장 |   중  |
|   1  |    ㄴ    |  팀장  |   상  |
|   2  |    ㄴ    |  사원  |   하  |
|   3  |    ㄱ    |  팀장  |   상  |

다음과 같은 테이블이 있다하자.

기본키인 '1' 사번, 'ㄱ' 프로젝트(A)일 때, 역할(B)는 부팀장이고, 역할(B)일 때, 고가(C)는 '중'이 된다.

즉, A->B 이고, B->C일 때, A->C가 된다.

이를 이런 식으로 이해한다면 제 3 정규화가 되지 않은 릴레이션을 찾아내기 껄끄럽다고 생각할 수 있다.

따라서 다르게 접근하면 훨씬 쉽다.

위 테이블에서 `고가`는 결국 `역할`에 `의존적`이다.

역할은 기본키가 아니며, 고가는 해당 테이블의 PK인 사번+프로젝트에 의존적이지 않다.

따라서, 이를 따로 테이블로 구분해주어야 한다는 것이다.

좀더 정리해서 `기본키에 전적으로 의존하지 않고 키가 아닌 일반 칼럼에 의존하는 칼럼을 제거시켜 원래의 제자리에 위치시키는 것이다.`

따라서 제 3 정규화를 한다면 다음과 같다.

| 사번 | 프로젝트 |  역할  |
|:----:|:--------:|:------:|
|   1  |    ㄱ    | 부팀장 |
|   1  |    ㄴ    |  팀장  |
|   2  |    ㄴ    |  사원  |
|   3  |    ㄱ    |  팀장  |

|  역할  | 고가 |
|:------:|:----:|
| 부팀장 |  중  |
|  팀장  |  상  |
|  사원  |  하  |

[출처 : http://clearpal7.blogspot.kr/2016/07/3.html](http://clearpal7.blogspot.kr/2016/07/3.html)

---

##### BCNF 정규화

---

여기부터는 흔히 잘 설명하지 못하는 부분이다.

제대로 알아두기로 하자.

흔히, BCNF 정규화는 제 3 정규화를 강화한 버전이라고 한다.

**BCNF 정규화** 는 `결정자가 아닌 함수 종속 제거`한 것을 말한다.

즉 다시 말해, `모든 결정자가 후보키 집합에 속한 정규형`이라 할 수 있다.

먼저, **후보키** 란, 수퍼키중에서 유일성, 최소성을 만족하는 것으로 기본키가 될 수 있는 것을 말한다.

그럼 **결정자** 가 무엇인지 알아보자.

**결정자** 란, `하나로 정해진 상태`를 말한다.

X->Y 일때, X가 바로 결정자 다.

[출처 : http://sjs0270.tistory.com/68](http://sjs0270.tistory.com/68)

그런데 앞선 제 3 정규화 예시에서 `역할`이 결정자냐 하면 그렇지 않다.

역할이 변한다고 해서, 사번과 프로젝트에 영향을 끼치진 않으며, 해당 튜플을 결정짓지 않기 때문이다.

즉, 제 3 정규화를 진행하면서 BCNF에 대해 생각할 상황이 아니게 된 것이다.

그럼 다른 예시를 통해 BCNF를 알아보자.

|  학생  |  과목  |   교수  | 학점 |
|:------:|:------:|:-------:|:----:|
| 홍길동 |  수리  |  James  |   A  |
| 김민희 |  언어  |  Kevin  |   B  |
| 최철수 | 외국어 | Scholes |   A  |
| 정만득 |  수리  |  James  |   B  |

먼저, 해당 과목을 가르치는 교수는 한명으로 유일하며, 학생 + 과목이 해당 릴레이션의 PK라 하자.

즉, 학생 + 과목으로 해당 튜플에 유일성을 만족시키므로, 결정자이면서 후보키(PK이므로)를 만족한다.

그럼 교수를 보자.

교수는 한 과목을 가르치는 유일한 사람이다.

따라서 다음과 같은 문제가 생긴다.

1. 교수만 변경할 수 없고 과목도 변경이 되어야 한다. (갱신 이상)
2. 새로운 과목과 교수가 생겼으나, 해당 과목을 듣는 사람이 없다면 해당 테이블에 넣을 수도 없다.(삽입 이상)
3. 최철수 학생이 사라지면, 해당 교수도 함께 사라진다.(삭제 이상)

즉, 교수가 `결정자`이지만 `후보키`가 아니라 위와 같은 문제가 생긴다.

따라서, 다음과 같이 나누어 주어야 한다.

|  학생  |   교수  | 학점 |
|:------:|:-------:|:----:|
| 홍길동 |  James  |   A  |
| 김민희 |  Kevin  |   B  |
| 최철수 | Scholes |   A  |
| 정만득 |  James  |   B  |

|   교수  |  과목  |
|:-------:|:------:|
|  James  |  수리  |
|  Kevin  |  언어  |
| Scholes | 외국어 |

---

##### 제 4 정규화

---

**제 4 정규화** 는 `다치 종속 제거`를 한 것을 말한다.

이제 `다치 종속`에 대해 알아보자.

이는 간단히 N:M 관계를 없애는 것이다.

| 학번 |  이름  | 과목번호 | 과목명 |
|:----:|:------:|:--------:|:------:|
|   1  | 홍길동 |    S1    |  수리  |
|   1  | 홍길동 |    S2    |  언어  |
|   2  | 최철수 |    S1    |  수리  |
|   3  | 정만득 |    S3    | 외국어 |

다음과 같은 테이블이 있다하자.

이는 N:M 을 이루고 있기 때문에 분리해야 한다.

| 과목번호 | 과목명 |
|:--------:|:------:|
|    S1    |  수리  |
|    S2    |  언어  |
|    S3    | 외국어 |

| 학번 |  이름  |
|:----:|:------:|
|   1  | 홍길동 |
|   2  | 최철수 |
|   3  | 정만득 |

| 학번 | 일련번호 | 과목번호 |
|:----:|:--------:|:--------:|
|   1  |     1    |    S1    |
|   1  |     2    |    S2    |
|   2  |     1    |    S1    |
|   3  |     1    |    S3    |

다음과 같이 1:N, M:1 관계로 나누어 주어야 한다.

---

##### 제 5 정규화

---

**제 5 정규화** 는 사실 실무에서 잘 쓰지 않는다고 한다.

그래도 알아보도록 하자.

제 5 정규화는 `조인 종속성 이용`하는 정규화이다.

즉, `모든 조인 종속이 후보키를 통해서만 성립되는 정규형`이라고 할 수 있다.

![SQL 조인](https://www.codeproject.com/KB/database/Visual_SQL_Joins/Visual_SQL_JOINS_orig.jpg)

일단 조인에 대해서 표를 보며 정리를 하고, 제 5 정규화에 대해 보도록 하자.

제 5 정규화를 성립하려면, 릴레이션 R에서 R의 프로젝션들인 X,Y,...,Z들을 자연조인 했을 때, R이 되어야 한다.

| OJT | 사내강사 |   교제   |
|:---:|:--------:|:--------:|
|  DB |     A    |  DB이론  |
|  DB |     B    |  DB이론  |
|  DB |     B    | 실습교제 |

다음과 같은 테이블이 있다고 하자.

이를 2가지 테이블로 나누었을 때,

| OJT |   교제   |
|:---:|:--------:|
|  DB |  DB이론  |
|  DB | 실습교제 |


| OJT | 사내강사 |
|:---:|:--------:|
|  DB |     A    |
|  DB |     B    |

와 같이 나눌 수 있다.

이를 자연 조인할 경우,

| OJT | 사내강사 |   교제   |
|:---:|:--------:|:--------:|
|  DB |     A    |  DB이론  |
|  DB |     A    | 실습교제 |
|  DB |     B    |  DB이론  |
|  DB |     B    | 실습교제 |

다음과 같이 나온다.

그럼 한 튜플이 잘못 나온것을 볼 수 있다.

이를 해결하려면,

| 사내강사 |   교제   |
|:--------:|:--------:|
|     A    |  DB이론  |
|     B    |  DB이론  |
|     B    | 실습교제 |

위와 같은 테이블을 추가해 자연조인을 해야한다.


---

### 간단한 알고리즘

---

간단한 알고리즘 문제를 물을 수 있다.

일단 정렬은 정리하고 가자.

---

#### Quick Sort

---

**Quick Sort** 의 중요한 점은 **분할 정복** 을 한다는 것과, **수색 점멸** 방법을 사용한다는 것이다.

즉, 분할해서 처리하며, 이를 처리할 때, 왼쪽 그리고 오른쪽에서 해당사항이 있을 때까지 수색하며 그 값을 처리하는 방식이다.

코드는 다음과 같다.

``` C++

void Swap(int* Left, int* Right){
    int tmp = * Left;
    * Left = * Right;
    * Right = tmp;
}

int Partition(int* DataSet, int Left, int Right){
    int First = Left;
    int Pivot = DataSet[First];
    ++Left;
    while(Left <= Right){
        while(DataSet[Left] <= Pivot && Left < Right)
            ++ Left;
        while(DataSet[Right] > Pivot && Left <= Right) //right는 후에 왼쪽 녀석의 마지막이 되야 하므로 같다도 포함해서 빼줘야 함
            -- Right;
        if(Left < Right)
            Swap(&DataSet[Left], &DataSet[Right]);
        else
            break;
    }
    Swap(&DataSet[First], &DataSet[Right]); //왼쪽 녀석의 마지막이니 right를 넣는것
    return Right;
}

void QuickSort(int* DataSet, int Left, int Right){
    if(Left < Right){
        int Index = Partition(DataSet, Left, Right);

        QuickSort(DataSet, Left, Index - 1);
        QuickSort(DataSet, Index + 1, Right);
    }
}

```

---

#### Merge Sort

---

다음은 병합 정렬이다.

이 역시 기본은 **분할 정복** 이다.

그러나 병합 정렬은 속도를 개선하기 위해 외부 메모리를 사용한다.

사실 병합 정렬의 손코딩은 매우 까다롭기 때문에 나오지 않을 가능성이 높지만, 그 기본 성격을 제대로 이해하고 코드도 이해하고 있자.

```C++

#include <stdio.h>
#define LEN 9

void merge_sort(int num[],int start, int end);
void merge(int num[], int start, int mid, int end);
void tracer(int num[],int len);

int main(void){

    int testArr[LEN] = {485,241,454,325,452,685,498,890,281};
    merge_sort(testArr, 0, LEN-1);
}

void merge_sort(int num[],int start, int end){ // Array를 두개의 덩어리로 나눔
    int median = (start + end)/2; // 중간값 설정
    if(start < end){ // 덩어리의 원소가 하나일 때까지
        merge_sort(num, start, median);
        merge_sort(num, median+1, end); // 각각의 덩어리로 재귀함수 호출
        merge(num, start, median, end); // 각각의 덩어리를 뭉치면서 정렬
    }
}

void merge(int num[], int start, int median, int end){
    int i,j,k,m,n;
    int tempArr[LEN]; // 임시로 데이터를 저장할 배열
    i = start; // 앞의 덩어리의 시작 Index
    j = median+1; // 뒤의 덩어리의 시작 Index
    k = start; // 임시 배열의 시작 Index

    while (i <= median && j <= end){
        tempArr[k++] = (num[i] > num [j]) ? num [j++] : num [i++];
        //작은 숫자를 찾아 임시 배열에 넣는다. 어느쪽 덩어리든 Index의 끝에 닿으면 빠져나온다.
    }

    // 아직 배열에 속하지 못한 부분들을 넣기 위한 부분
    m = (i > median) ? j : i; // 아직 원소가 남아있는 덩어리가 어디인지 파악
    n = (i > median) ? end : median; // 마찬가지로, for문의 끝 Index를 정하기 위함임

    for (; m<=n; m++){ // 앞에서 구한 m, n으로 배열에 속하지 못한 원소들을 채워넣음
        tempArr[k++] = num[m];
    }

    for (m=start; m<=end; m++){
        num[m] = tempArr[m]; // 임시 배열에서 원래 배열로 데이터 옮기기
    }
    printf("Merging: %d ~ %d & %d ~ %d\n",start,median,median+1,end);
    tracer(num,LEN);
}

void tracer(int num[],int len){
    int i;
    for(i=0;i<len;i++){
        printf("%d\t",num[i]);
    }
    printf("\n\n");
}


```

---

#### GCD

---

간단하다. 그냥 외워도 되고, 유클리드 호제법을 이해하도록 하자.

``` C++
int GCD(int a, int b){
    return b == 0 ? a : GCD(b, a%b);
}

```

---

#### Quick Selection

---

[출처 : http://hackability.kr/entry/Quick-Selection%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-On-%EC%84%A0%ED%83%9D-%EB%B0%A9%EB%B2%95](http://hackability.kr/entry/Quick-Selection%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-On-%EC%84%A0%ED%83%9D-%EB%B0%A9%EB%B2%95)

**Quick Selection** 은 **N 번째로 큰수** 를 찾을 때, Pivot에 때라 평균적으로, O(N)으로 찾을 수 있는 방법이다.

보통 전체를 Sorting 한다고 하면 NlogN이 걸린다고 한다.

그러나, N번째로 큰 수를 찾는 것이 O(N)만에 할 수 있다고 한다면 매우 효율이 올라가는 작업일 것이다.

가끔 면접 문제로 나오기 때문에 알아두면 좋을 것이다.

퀵소트 변형 정도로 알면 된다.

``` C++
#include <iostream>
#include <stdlib.h>
#include <time.h>
using namespace std;

#define NUM 15

//배열, 시작값, 크기, 등수
//l, l+1 ,l+2
void Selection(int* A,int i,int j,int k)
{
    int left = i;
    int right = j+1;
    int pivot = A[i];
    int temp;

    while(left<right)
    {
        do
        {
            right--;
        }while(A[right] > pivot && left<right);

        do
        {
            left++;
        }while(A[left] < pivot && left<right);

        if(left<right)
        {
            temp = A[left];
            A[left] = A[right];
            A[right] = temp;
        }
        else//left>=right
        {
            temp = A[i];
            A[i] = A[right];
            A[right] = temp;

            //디버깅 출력

            printf("left : %d, right : %d, pivot : %d, k : %d, A[k-1] : %d\n",left,right,pivot,k,A[k-1]);

            int count=1;
            for(int index=0;index<NUM;index++)
            {
                printf("%3d",count++);
            }
            cout<<endl;
            for(int index=0;index<NUM;index++)
            {
                printf("%3d",A[index]);
            }
            cout<<endl;
            cout<<endl;


            if(right == k-1)
            {
                printf("%d번째 등수는 %d이다.\n",k,A[k-1]);
                return;
            }
            else if(right < k-1)
            {
                Selection(A,right+1,j,k);
            }
            else
            {
                Selection(A,i,right-1,k);
            }
        }
    }
}

int main()
{
    srand((unsigned int)time(NULL));
    int arr[15];
    int count=1;
    int K=3;
    for(int i=0;i<NUM;i++)
    {
        printf("%3d",count++);
    }
    cout<<endl;
    for(int i=0;i<NUM;i++)
    {
        arr[i] = rand()%100+1;
        printf("%3d",arr[i]);
    }
    cout<<endl<<endl;

    Selection(arr,0,NUM-1,K);

    return 0;
}
```

---

#### 압축 알고리즘

---

트리를 이용한 압축 알고리즘은 모 IT 기업 면접 문제로 나왔던 것이다.

제대로 알고 넘어가도록 하자.

흔히 **허프만 코드** 라고 하며, 자주 쓰이는 문자에 가장 작은 bit 를 할당하고 한두번 쓰이는 문자에는 큰 bit 를 할당한다라는 것이다.

예를 들어 `CDDCACBCBCCCBBCDA` 문자열이 있다고 하자.

일단 해당하는 빈도수를 체크한다.

`A - 2, B - 4, C - 8, D - 3`

빈도수 대로 나열한다면, C,B,D,A 순이 될 것이다.

그럼 가장 낮은 2개 (D,A)부터 묶어 그 수를 체크한다. (D+A = 5)

다시 빈도 수로 나열한다.

`C, (D+A), B`

다시, 가장 낮은 2개를 묶는다. ((D+A) + B = 9)

다시 빈도 수로 나열한다.

`((D+A) + B), C`

이를 묶어 트리로 완성한다.

![허프만 코드 트리](http://cfs4.tistory.com/upload_control/download.blog?fhandle=YmxvZzUwMDg3QGZzNC50aXN0b3J5LmNvbTovYXR0YWNoLzAvMDgwMDAwMDAwMDAyLnBuZw%3D%3D)

그럼 최종 트리를 완성할 수 있다.

![허프만 코드 최종 트리](http://cfs4.tistory.com/upload_control/download.blog?fhandle=YmxvZzUwMDg3QGZzNC50aXN0b3J5LmNvbTovYXR0YWNoLzAvMDgwMDAwMDAwMDAzLnBuZw%3D%3D)

이를 정리하면 압축 알고리즘이 완성된다.

![허프만 코드 압축 비트](http://cfs6.tistory.com/upload_control/download.blog?fhandle=YmxvZzUwMDg3QGZzNi50aXN0b3J5LmNvbTovYXR0YWNoLzAvMDgwMDAwMDAwMDAyLnBuZw%3D%3D)

`A 는 001 이 되는 것이다.`


[출처 : http://wooyaggo.tistory.com/95](http://wooyaggo.tistory.com/95)

---

### OS

---

OS 부분은 나오는 경우가 꾀나 많다.

잘 정리해서 실수하지 않도록 하자.

---

#### Process와 Thread

---

**Process** 는 보통 실행중인 프로그램이라는 말로 정리한다.

좀더 구체적으로 말해보면, `운영체제로부터 자원을 할당받은 작업의 단위`라고 할 수 있다.

쓰레드는 `프로세스 내에서 공용의 메모리를 가진 CPU 작업의 기본 단위`이다.

즉, `프로세스가 할당받은 자원의 실행의 단위`라고 할 수 있다.

쓰레드는 아무래도 프로세스를 생성해 자원을 할당하는 시스템콜이 줄어든다.

즉, 프로세스간 통신비용보다 쓰레드간 통신비용이 훨씬 줄어든다.

그러나 쓰레드간 자원공유는 전역 변수를 사용하다 보니 동기화 문제가 있다.

---

##### 사용자 Thread, 커널 Thread

---

**커널 Thread** 는 커널이 주체로 Thread를 생성하기 때문에 안전성과 기능을 보장한다.

그러나 유저 모드와 커널 모드를 왔다갔다하므로 Context Switching이 자주일어나게되어 효율이 떨어진다.

**사용자 Thread** 는 커널이 Thread의 존재를 모른다.

즉, Context Switching이 전혀 일어나지 않는다.

따라서 하나의 Thread라도 커널에 의해 블락이 되면 프로세스 자체가 블락되기 때문에 해결하기 까다롭다. (안전성에 문제가 생길 수 있다)

---

#### 프로세스 스케줄링

---

**스케줄링** 은 `프로세스가 생성되어 실행될 때 필요한 시스템의 여러 자원을 해당 프로세스에게 할당하는 작업`이다.

스케줄링은 CPU나 자원을 효율적으로 사용하기 위한 정책이며, 공정성, 처리율 증가, CPU 이용률 증가 등의 목적을 가진다.

기법에 있어서 크게 2가지로 나눈다.

1. 비선점 스케줄링
2. 선점 스케줄링

하나씩 알아가 보자.

---

##### 비선점 스케줄링

---

**비선점 스케줄링** 은 이미 할당된 CPU를 다른 프로세스가 강제로 빼앗아 사용할 수 없는 스케줄링 기법을 말한다.

즉, 프로세스가 CPU를 할당받으면 해당 프로세스가 완료될 때까지 CPU를 사용하게 된다.

종류는 FCFS, SJF, 우선순위 등이 있다.

**FCFS** 의 경우, FIFO라고도 한다. 즉, 들어온 순서대로 처리하는 것이다.

**SJF** 의 경우, 준비상태 큐에 있는 프로세스 중 가장 짧은 작업시간의 프로세스를 먼저 처리하는 것이다.

**우선순위** 의 경우, 프로세스마다 우선순위를 부여해 가장 높은 프로세스에게 먼저 CPU를 할당한다.

동일한 경우, FCFS와 동일하게 되며, 우선순위가 매우 낮으면 무기한 연기 혹은 기아 상태가 발생할 수 있다.

따라서 **Aging** 기법을 이용해, 우선순위를 높이는 방법도 적용할 수 있다.

---

##### 선점 스케줄링

---

**선점 스케줄링** 은 프로세스 중 우선순위가 가장 높은 프로세스에게 먼저 CPU를 할당하는 것이다.

즉, 현재 상태에 따라 CPU를 뺏아올수 있다.

종류는 SRT, RR 등이 있다.

**SRT** 는 현재 프로세스들과 새로 들어온 프로세스 중 가장 짧은 실행시간을 요구하는 프로세스에게 먼저 CPU를 할당하는 것이다.

**RR** 은 Round Robin 방식으로, 각 프로세스의 시간 할당량에 의해 FCFS로 처리하되, 시간 할당량동안만 실행한 후, 실행이 완료되지 않으면 다음 프로세스에게 넘겨주고 **준비상태 큐** 의 가장 뒤로 가는 방식이다.


---

#### 크리티컬 섹션, 뮤텍스, 세마포어

---

멀티 프로세스 혹은 멀티 쓰레드에 있어서 가장 자주 물어보는 개념일 것이다.

프로그래밍 적으로 접근하면 멀티 쓰레드의 동기화에서 사용된다.

먼저 **크리티컬 섹션(임계구역)** 의 이론적인 내용을 알아보면 다중 프로그래밍 운영체제에서 여러 개의 프로세스가 공유하는 데이터 및 자원에 대해 어느 한 시점에서는 하나의 프로세스만 자원 또는 데이터를 사용하도록 지정된 공유 자원(영역) 이다.

**뮤텍스(상호배제)** 는 특정 프로세스가 공유 자원을 사용하고 있을 경우 다른 프로세스가 해당 공유 자원을 사용하지 못하게 제어하는 기법이다.

즉, 여러 프로세스가 동시에 공유 자원을 사용할 때, 각 프로세스가 번갈아가며 공유 자원을 사용하게 하면서 Critical Section(임계 구역)을 유지하는 기법이다.

**세마 포어** 는 각 프로세스에 제어 신호를 전달해 순서대로 작업을 수행하도록 하는 기법이다.

즉, 공유 자원의 갯수를 이용해 지정된 수보다 작거나 같을 때는 허용하며 그 수를 초과할 때는 차단하는 방법이다.


프로그래밍적으로 접근해 보면, **Critical Section** 은 유저 영역 메모리에서 동기화 시킬 때 사용된다.

앞서 **임계구역** 에 대한 설명은 말 그대로 임계구역의 의미를 말한 것이고, 프로그래밍 적으로 접근했을 때는 **Critical Section 기법** 이라는 명명이 붙어진 작업을 의미한다.

하여튼 유저 영역이라는 것을 생각해 본다면 한 프로세스 내의 쓰레드간의 동기화에 사용함을 알 수 있다.

또한, 가볍고 간단히 쓸수 있는 동기화 객체이다.

**뮤텍스** 는 그와 달리 커널 객체이므로, 그러므로 크리티컬 섹션보다 무겁다.

크리티컬 섹션이 한 프로세스 내의 쓰레드 사이에서만 동기화가 가능한 반면, 뮤텍스는 여러 프로세스의 스레드 사이에서 동기화가 가능하다.

또한, 다중 프로세스 실행을 방지할 수 있다. 이는 크리티컬 섹션에서는 할 수 없는 방법이다.

**세마 포어** 역시 커널 객체로, 세마포어는 지정된 수만큼의 쓰레드가 동시에 실행되도록 동기화하는 것이 가능하다.

자세한 사항은 다음을 참고하자.

[출처 : http://egloos.zum.com/sweeper/v/2815499](http://egloos.zum.com/sweeper/v/2815499)

---

#### 메모리 관리

---

메모리 관리는 꾀 여러가지 있다.

보조기억장치와 주기억장치, 가상기억장치, 단편화 등 중요한 개념이 많다.

하나씩 정리해 보도록 하자.

---

##### 배치 전략

---

`새로 반입된 프로그램이나 데이터를 주기억 장치에 어디에 위치 시킬 것인지 결정하는 전략`이다.

1. First Fit
2. Best Fit
3. Worst Fit

으로 생각할 수 있다.

**First Fit** 의 경우, `프로그램이나 데이터가 들어갈 수 있는 크기의 빈 영역 중 가장 처음 분할 영역에 배치 하는 방법`이다.

**Best Fit** 의 경우, `프로그램이나 데이터가 들어갈 수 있는 크기의 빈 영역 중 단편화를 가장 작게 남기는 분할 영역에 배치 하는 방법`이다.

**Worst Fit** 의 경우, `프로그램이나 데이터가 들어갈 수 있는 크기의 빈 영역 중 단편화를 가장 많이 남기는 분할 영역에 배치 하는 방법`이다.

**단편화** 는 분할된 주기억장치에 프로그램을 할당하고 반납하는 과정을 반복하면서 사용되지 않고 남는 기억장치의 빈공간 조각을 의미하며, 내부 단편화 외부 단편화가 있다.

---

##### 할당 기법

---

먼저, 주기억장치는 `프로그램이나 데이터를 실행하기 위해 주기억장치에 어떻게 할당할 것인지`에 대해 **할당 기법** 들을 사용한다.

이는, **연속 할당 기법** (단일 분할 할당, 다중 분할 할당)과 **분산 할당 기법**(페이징, 세그먼테이션)이 있다.

**단일 분할 할당** 의 경우, 초기 운영체제의 방법이며 `오직 한 명의 사용자만이 주기억장치의 사용자 영역을 사용하는 것`이다.

**오버레이** (주기억 장치보다 큰 프로그램을 실행 할 때, 불필요한 조각이 위치한 장소에 새로운 프로그램의 조각을 중첩하여 적제하는 방법), **스와핑** (하나의 프로그램 전체를 할당하여 사용하다, 다른 프로그램과 교체하는 방법)이 있다.

**다중 분할 할당 기법** 의 경우, 고정 분할 할당, 가변 분할 할당이 있으며,

**고정 분할 할당** 의 경우, `프로그램 할당 전에 운영체제가 주기억장치의 사용자 영역을 여러개의 고정 크기로 나눈 후 준비상태 큐에서 준비중인 프로그램을 각 영역에 할당해 수행하는 방법`이다.

따라서 일정한 크기의 분할 영역에 다양한 크기의 프로그램이 할당되어 내부 단편화 혹은 외부 단편화가 빈번히 일어난다.

**가변 분할 할당** 은 프로그램에 따라 다르게 할당하여 단편화를 줄이는 방법으로, 효율적이며, 제약이 적지만 영역과 영역 사이에 단편화가 발생할 수 있다.

즉, 한번 할당하고 해소된 영역에 새로운 프로그램이 들어가게 되면 영역 크기에 따라 단편화가 발생할 수 있다.

**가상기억장치** 는 `보조기억장치의 일부를 주기억장치처럼 사용하는 것으로, 용량이 작은 주기억장치를 마치 큰 용량을 가진 것처럼 활용하는 것`이다.

따라서 `블록 단위로 나누어 가상기억장치에 보관해두고 프로그램 실행 시 요구되는 블록만 주기억장치에 할당하여 처리`한다.

`주소 변환 작업`이 필요하며, 블록 단위로 나누어 활용하므로 `연속 할당 방식에 발생하는 단편화를 해결`할 수 있다.

구현 방법으로는 페이징, 세그멘테이션 기법이 있다.

**페이징** 은 가상기억장치에 보관되어 있는 프로그램과 주기억장치의 메모리 영역을 동일한 크기의 페이지로 나누어 적재하는 기법이다.

주기억장치에 페이지 크기로 나누어진 영역을 페이지 **프레임** 이라고 부른다.

주소 변환을 위해 페이지 맵 테이블을 요구한다.

외부 단편화는 발생하지 않지만 내부 단편화는 발생한다.

ex> 페이지 크기를 4KB라 하고, 프로그램이 17KB라 하면 마지막 페이지의 용량은 1KB가 되며 내부 단편화 3KB가 발생한다.

가상메모리를 물리주소로 변환하는 오버헤드가 발생한다.

프로그램이 참조한 메모리가 주기억장치에 없는 `페이지 부재` 발생할 수 있다.

**세그멘테이션** 은 가상기억장치에 보관되어 있는 프로그램을 다양한 크기의 논리적 단위로 나누어 적재하는 기법이다.

세그먼트 맵 테이블을 요구한다.

다른 세그먼트에 할당할 영역을 침범하지 않게 장치 보호기(Storage Protection Key)를 요구한다.

내부 단편화는 발생하지 않지만 외부 단편화가 발생할 수 있다.

ex> 나누어진 단위가 20KB인데, 남은 주기억장치 크기가 17KB라면 17KB의 외부 단편화가 발생한다.

**페이지 교체 알고리즘** 은 `페이지 부재(page fault)`가 발생했을 때 가상기억장치의 필요한 페이지를 주기억장치에 적재해야 하는데, 이 때 주기억장치의 모든 페이지 프레임이 사용중이라면 어떻게 교체할것인지 결정하는 알고리즘이다.

즉, 필요한 내용이 주기억장치에 없는데, 이미 주기억 장치의 프레임을 모두 사용중이라면 어떻게 교체할 것인지를 의미한다.

그 종류는 OPT, FIFO, LRU, LFU 등이 있다.

**OPT** 는 최적교체로 앞으로 가장 오랫동안 사용하지 않을 페이지를 교체하는 것으로 실현 가능성이 희박한 이상적 방법이다.

**FIFO** 는 가장 먼저 들어와있던 페이지를 교체하는 방법이다.

**LRU** 는 가장 예전에 교체한 페이지를 교체하는 방법이다.

**LFU** 는 가장 적게 교체한 페이지를 교체하는 방법이다.

**페이지 크기** 는 작을 수록, 단편화가 감소되고 주기억장치에 이동하는 시간이 감소되며 Locality에 더 일치할 수 있으므로 기억장치에 효율이 증가하고 Working Set(Locality에 의해 일정 시간동안 자주 참조하는 페이지들의 집합)를 효율적으로 유지할 수 있지만,

페이지 맵 테이블이 커지고 매핑 속도가 늘어나며, 디스크 접근이 많아져 입 출력 시간이 늘어난다.

페이지 크기가 크다면 이와 반대다.

**Locality** 는 프로세스가 실행되는 동안 주기억장치를 참조할 때 일부 페이지만 집중적으로 참조하는 성질을 말한다.

**쓰레싱** 은 프로세스 처리 시간보다 페이지 교체에 소요되는 시간이 많아지는 것을 말하며, 페이지 부재를 줄이고, Working Set을 유지하는 방안이 필요하다.

---

### 기본 CS

---

기본적으로 알고 있어야 할 CS를 정리해 보자.

---

#### 절차지향프로그래밍과 객체지향프로그래밍

---

**절차지향, 구조적 프로그래밍(C)**

초창기에 많이 사용한 방법으로 순차적 프로그래밍이라고도 한다.

해야할 작업을 순서대로 코딩을 한다.

구조적 프로그래밍에서는 함수 단위로 구성되며 기능별로 묶어놓은 특징이 있다.

**객체지향 프로그래밍(JAVA, C++, C#)**

주 구성요소는 클래스와 객체이다.

그리고 상속과 다형성을 특징으로 들 수 있다. 클래스를 활용하여 각각의 기능별로 구성이 가능하며, 이를 나중에 하나로 합쳐서 프로그램의 완성이 가능하다.

객체 별로 개발이 가능하기에 팀 프로젝트를 하기에도 유리한 장점을 가지고 있다.

또한 코드의 재사용이 가능하며, 오류 발생 가능성이 적고 안정성이 높다.

**함수형 프로그래밍** 은 다음을 참고하자.

[출처 : https://medium.com/@jooyunghan/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-fab4e960d263](https://medium.com/@jooyunghan/%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-fab4e960d263)

---

#### MVC 패턴

---

Model, View, Controller 를 의미하며

**Model** 은 데이터 혹은 데이터 처리 영역

**View** 는 결과 화면을 만들어 내는데 사용하는 자원

**Controller**  요청을 처리하고 Model과 View의 중개자 역할