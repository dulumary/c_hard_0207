## 문제) - 동적 메모리 할당

### 1. 사이즈 확인

* int  변수 73개, char 변수 43개, double 변수 12개 의 총 byte 수를 구하여 출력하세요.

> 출력 예시 

```
431 byte
``` 

### 2. 배열 값 저장

* 아래와 같이 동적으로 할당된 배열에 값을 입력 받아서 저장 하고, 이를 출력 하세요. 

`int *inputArray = (int *)malloc(sizeof(int) * 3);`

* 배열의 크기 만큼 모두 저장 하세요.

> 입력 예시 

```
수를 입력 하세요 : 45
수를 입력 하세요 : 3
수를 입력 하세요 : 1
```

> 출력 예시 

```
45 3 1 
```

### 3. 동적 배열 만들기
* 아래 주어진 배열과 똑같은 배열을 동적 할당을 이용해서 만들고, 출력 하세요. 

`int array[4] = {1200, 1500, 1000, 2500};`

> 출력 예시 

```
1200 1500 1000 2500 
```

### 4. 수 입력
* 입력 받은 갯수만큼 수를 저장 하고, 출력 하는 프로그램을 만드세요. 
* 몇 개의 수를 입력 받을지 입력 받으세요. 
* 입력 받을 수 만큼 반복문을 통해 입력 받고, 배열에 저장하여 이를 출력 하세요.

> 입력 예시 

```
입력할 갯수를 입력 하세요 : 3
수를 입력 하세요 : 9
수를 입력 하세요 : 5
수를 입력 하세요 : 3
```

> 출력 예시 

```
9 5 3 
```

### 5. 단어 합치기

* 두개의 단어를 차례로 입력 받고, 이 단어를 합쳐서 저장 하는 문자열 변수를 만들고 그 결과를 출력 하세요. 
  * 입력 받는 단어의 최대 길이는 16입니다. (배열로 만들어서 사용하세요.)
* 두 단어 사이는 ,(쉼표)로 구분 되게 저장 하세요. 
* 합쳐진 문자열을 저장하는 문자열 변수를 동적 할당을 통해서 메모리 낭비가 없도록 하세요. 
* hint ) sprintf 함수를 사용 하세요

> 입력 예시 

```
단어를 입력 하세요 :  hey
단어를 입력 하세요 :  come
```

> 출력 예시 

```
hey,come
```


[정답 보기](test01.c)
