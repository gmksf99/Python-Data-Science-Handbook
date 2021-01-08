# NumPy 
조밀한 데이터 버퍼에서 저장하고 처리하는 효과적인 인터페이스를 제공

# 데이터 

### 리스트 
- 문자열 리스트 <br>
  `In[1] : L = [str(c) = for c in range(10)]` <br>
  `Out[1] : ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']`
  
- 서로 다른 데이터 타입 <br>
`In[2] : L2 = [True, "2", 3.0, 4]` <br>
`Out[2] : [bool, str, float, int]`

### numpy패키지의 ndarray 개체
배열의 모든 요소가 같은 타입이여야 함. -> 고정 타입을 가짐
타입이 일치하지 않으면 가능한 경우 상위 타입을 취함.

- np.array(시작, 끝, 간격)

	- 정수 배열 <br>
`In[3] : np.array([1, 4, 2, 3.14, 6])` <br>
`Oup[3] : array([1. , 4. , 2. , 3.14, 6. ])`

	- 다차원 배열 <br>
`In[4] : np.array([range(i, i+3) for i in [2, 4, 6]])` <br>
`Out[4] :array([[2, 3, 4], [4, 5, 6], [6, 7, 8]])`

- np.random.random((배열))
	
	- 3x3 배열 <br> 
`In[5] : np.random.random((3, 3))` <br>
`Out[5] : array([[0.11721156, 0.27321042, 0.03939562],` <br>
`[0.33073537,0.14793991, 0.08647627],` <br>
`[0.50834328, 0.24414057, 0.68788801]])` 

- np.random.normal(평균, 표준편차, (배열))

- np.random.randint(시작, 끝, (배열))

# 배열 슬라이싱

- 슬라이싱 : x[시작:끝:간격]
- 1차원 배열: `array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])`	  
	
	- 첫 다섯 개 요소 <br>
`In[6] : x[:5]` <br>
`Out[6] : array([0, 1, 2, 3, 4])` 

	- 인덱스 5 다음 요소들 <br>
`In[7] : x[5:]`  <br>
`Out[7] : array([5, 6, 7, 8, 9])` 

	- 시작부터 2칸 간격으로 끝까지 <br>
`In[8] : x[::2]`  <br>
`Out[8] : array([0, 2, 4, 6, 8])` 

	- 인덱스 1부터 시작해 3칸 간격으로 끝까지 <br>
`In[9] : x[1::3]`  <br>
`Out[9] : array([1, 4, 7])` 

- 다차원 배열 : `array([[12, 5, 2, 4], [7, 6, 8, 8], [1, 6, 7, 7]])`

	- 2개의 행, 3개의 열 <br>
`In[10] : x[:2, :3]`  <br>
`Out[10] : array([[12,  5,  2], [ 7,  6,  8]])` 

	- 모든 행,  2칸 간격으로 열 <br>
`In[11] : x[:, ::2]` <br>
`Out[11] : array([[12,  2], [ 7,  8], [ 1,  7]])` 

	- 역 변환 <br>
`In[12] : x[::-1, ::-1]` <br>
`Out[12] : array([[ 7,  7,  6,  1], [ 8,  8,  6,  7], [ 4,  2,  5, 12]])` 

# 배열 연결 및 분할

 `x = np.array([1, 2, 3])` <br>
 `y = np.array([4, 5, 6])`

- 연결

	- 일차원 배열 연결(2개 이상도 가능/ 2차원 배열도 가능) <br>
`In[13] : np.concatenate([x, y])` <br>
`Out[13] : array([1, 2, 3, 4, 5, 6])` 

	- 혼합된 차원의 배열 연결 <br>
`z = np.array([4, 5, 6], [7, 8, 9])` <br>
`v = np.array([100], [100])`
		
		- 수직 : np.vstack() <br>
`In[14] : np.vstack([x, z])`  <br>
`Out[14] : array([[1, 2, 3], [4, 5, 6],[7, 8, 9]])` 

		- 수평 : np.hstack() <br>
`In[15] : np.vstack([z, v])` <br>
`Out[15] : array([[4, 5, 6, 100],[7, 8, 9, 100]])` 

<h2></h2>

`x = np.array([4, 5, 6, 100, 7, 8, 9, 100])`

- 분할

	- 일차원 배열 분할(인덱스 기준 앞 분할) <br>
`In[16] : x1, x2, x3 = np.split(x, [3,5])` <br>
`Out[16] : [4 5 6] [100 7] [8 9 100]`

	- 다차원 배열 분할 <br>
`x = np.array([[ 7,  7,  6,  1], [ 8,  8,  6,  7], [ 4,  2,  5, 12]])`
	
		- 수직 : np.vsplit <br>
		`In[17] : x1, x2 = np.vsplit(x, [2])` <br>
		`Out[17] : [[7 7 6 1] [8 8 6 7]] [[ 4  2  5 12]]`

		- 수평 : np.hsplit <br>
		`In[18] : x1, x2 = np.hsplit(x, [2])` <br>
		`Out[18] : [[7 7] [8 8] [4 2]] [[6 1] [6 7] [5 12]]`

# NumPy 유니버설 함수(Ufuncs)
| 연산자 | 대응 ufuncs | 설명 |
|--|--|--|
| + | np.add | 덧셈 |
| - | np.subtract | 뺄셈 | 
| - | np.negative | 음수 |
| * | np.multiply | 곱셈 |
| / | np.divide | 나눗셈 |
| // | np.floor_divide | 나눗셈(소수점 버림) |
| ** | np.power | 지수 |
| % | np.mod | 나머지 |
| ㅣ ㅣ | np.absolute / np.abs | 절대값 |

### 삼각함수 
| 함수 | 대응 ufuncs |
|--|--|
| sin | np.sin |
| cos | np.cos |
| tan | np.tan |
| 역 sin | np.arcsin |
| 역 cos | np.arccos |
| 역 tan | np.arctan |

### 지수/로그
| 함수 | 대응 ufuncs |
|--|--|
| 오일러의 수 e | np.exp |
| ln(x) | np.log |
| log2 | np.log2 |  
| log10 | np.log10 |
| exp(x)-1 | np.expm1 |
| log(1+x) | np.log1p |

### 집계
- 집계함수 : reduce 

	- 모든 배열의 요소 합 : np.add.reduce
	- 모든 배열의 요소 곱 : np.multiply.reduce

- 계산 중간 결과 저장 : accumulate <br>
`x = [1,2,3,4,5]`  <br>
`In[17] : np.multiply.accumulate(x)` <br>
`Out[17] : array([ 1,  3,  6, 10, 15])`	   	 

- 서로 다른 두 입력값의 모든 쌍에 대한 출력값 계산 : outer <br>
`In[18] : np.multiply.outer(x,x)` <br>
`Out[18] : array([[ 1,  2,  3,  4,  5],` <br>
`[ 2,  4,  6,  8, 10],` <br> 
`[ 3,  6,  9, 12, 15],` <br> 
`[ 4,  8, 12, 16, 20],` <br> 
`[ 5, 10, 15, 20, 25]])` 

- 기타 집계 함수

| 함수명 | NaN 안전모드 | 설명 |
|--|--| -- |
| np.sum | np.nansum | 요소의 합 계산 |
| np.prod | np.nanprod | 요소의 곱 계산 |
| np.mean | np.nanmean | 요소의 평균 계산 |
| np.std | np.nanstd | 표준 편차 계산 |
| np.var | np.nanvar | 분산 계산 |
| np.min | np.nanmin | 최솟값 찾기 |
| np.max | np.nanmax | 최댓값 찾기 |
| np.argmin | np.nanargmin | 최솟값 인덱스 찾기 |
| np.argmax | np.nanargmax | 최댓값 인덱스 찾기 |
| np.median | np.nanmedian | 요소의 중앙값 계산 |
| np.percentile | np.nanpercentile | 요소의 순위 기반 백분위 수 계산 |
| np.any | N/A | 요소 중 참이 있는지 검사 |
| np.all | N/A | 모든 요소가 참인지 검사 |

# 배열 정렬
`x = np.array([2,1,4,3,5])` <br>
- 빠른 정렬 : sort <br>
`In[19] : np.sort(x) / x.sort(x)` <br>
`Out[19] : array([1,2,3,4,5])`

- 정렬된 요소의 인덱스 반환 : argsort <br>
`In[20] : i = np.argsort(x)` <br>
`Out[20] : [1,0,3,2,4]` <br>
`In[21] : x[i]` <br>
`Out[21] : array([1,2,3,4,5])`

- 행/열 기준 정렬
	- 행 : `np.sort(배열, axis=1)`
	- 열 : `np.sort(배열, axis=0)`
