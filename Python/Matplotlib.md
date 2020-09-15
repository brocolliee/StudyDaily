## Matplotlib Library

- '빅데이터 서비스' 강의 들은 후 정리



### Matplolib

- Matplotlib을 사용한 데이터 시각화
  - 데이터의 구조와 패턴 파악에 용이
  - 사람이 가진 직관력을 극대화 할 수 있음
- Matplotlib을 사용하여 다양한 그래프를 그릴 수 있음 



### 선형 그래프

- 시간의 경과에 따라 값이 변하는 시계열 데이터에 사용

```python
import matplotlib.pyplot as plt
import seaborn as sns # data

flight = sns.load_dataset("flights") # flight에 데이터프레임 생성 (sns의 데이터 불러오기)

m = flight['year'] == 1949 # mask 생성, 1949년도인 부분에만 True 할당
f_1949 = flight[m] # 1949년에 해당하는 부분만 생성

fig = plt.figure()
# fig = plt.figure(figsize= (7,7)) # graph가 담긴 figure, figsize : 출력되는 가로, 세로 사이즈


# add_subplot parameter
# first - 전체 화면을 세로로 몇등분 할 것인지
# second - 가로로 몇 등분 할 것인지
# third - 앞에 나눈 화면에서 몇번째 칸에 그래프 작성 할 것인지
ax1 = fig.add_subplot(1,1,1) # 하나의 그래프를 그리기 위해 1,1,1을 입력
"""
## 두개의 그래프 그리기
ax1 = fig.add_subplot(2,1,1) # 세로로 2등분, 가로로 1등분, 첫번째 칸
ax2 = fig.add_subplot(2,1,2) # 2번째 칸
"""

ax1.set(title = '1949', xlabel = 'month' , ylabel = '# of passengers') #제목, x, y축 label

# plot paraemter
# first - x 축에 표시할 것 , second - y 축에 표시할 것
ax1.plot(f_1949['month'], f_1949['passengers']) # 선형 그래프 (but 글자가 겹쳐보임)
# x 축의 month의 앞의 세글자만 사용하기 위해서 아래와 같이 진행
# ax1.plot(f_1949['month'].str[0:3] + '.', f_1949['passengers'])

ax1.tick_params('x', rotation = 45) # 45도 만큼 x에 해당하는 label 회전

# 그래프가 전체 화면(figure)에 잘 보이지 않는 경우 figsize로 조절 혹은 tight_layout() 사용
plt.tight_layout() # 그린 그래프의 레이아웃 밑 사이즈를 자동으로 조절

plt.show()
```



```python
# 2개 그래프 그리기

# 첫번째 그래프
ax1 = fig.add_subplot(1,2,1)
ax1.set(title = '1949', xlabel = 'month' , ylabel = '# of passengers') 
ax1.plot(f_1949['month'].str[0:3] + '.', f_1949['passengers'])
ax1.tick_params('x', rotation = 45)

ax2 = fig.add_subplot(1,2,1)
ax2.set(title = '1949~1960', xlabel = 'month' , ylabel = '# of passengers')

# 두번째 그래프 - 월별 이용수 
f_all = flight.groupby('month').sum() # month로 묶어 sum
# ax2.plot(f_all['month'].str[0:3] + '.', f_all['passengers']) # month col 없음 오류 발생
ax2.plot(f_all.index.str[0:3] + '.', f_all['passengers']) 

plt.tight_layout() # 그린 그래프의 레이아웃 밑 사이즈를 자동으로 조절
```



### 히스토그램

```python
import matplotlib.pyplot as plt
import seaborn as sns # data

iris = sns.load_dataset("iris") # iris dataframe
fig = plt.figure()

ax1 = fig.add_subplot(1,1,1)

# 히스토그램 그리기

"""
# 임의의 구간으로 나눠줘 그린 히스토그램
ax1.hist(iris['petal_length']) # 히스토그램 그리기
"""
# 사용자가 구간을 지정
b = [] # 구간 리스트
for i in range(40):
    b.append(0.2 * i) 
ax1.hist(iris['petal_length'], bins = b)

ax1.set(title = 'petal_length') 

plt.show()
```



```python
# 두개 (종으로 나눠서 그리기)
iris_g = iris.groupby('species') # 종으로 나눔

ax1 = fig.add_subplot(1,2,1)
ax1.hist(iris['petal_length'], bins = b)
ax1.set(title = 'petal_length') 

ax2 = fig.add_subplot(1,2,1)
for name, group in iris_g:
	ax2.hist(group['petal_length'], bins = b ,label = name) # 현재 그래프의 이름 표시

ax2.set(title = 'petal_length species')
ax2.legend() # 범례 표시 (어떤 색이 어느 종에 해당하는지를 보여줌)

```



### 산점도

- 분포를 파악 및 상관 관계를 파악 할 수 있음.

```python
import matplotlib.pyplot as plt
import seaborn as sns # data

iris = sns.load_dataset("iris") # iris dataframe
iris_g = iris.groupby('species')

fig = plt.figure()

ax1 = fig.add_subplot(1,1,1)
for name, group in iris_g:
	ax1.scatter(group['petal_length'], group['petal_width'] ,label = name) # 산점도생성
    # parameter : first -  x좌표에서 사용할 데이터 , second - y 좌표 , label = 종 이름
    
ax1.set(title = 'petal_length vs petal_width', xlabel = 'petal_length' , ylabel = 'petal_width')

ax1.legend() # 각 종류에 따른 값을 
plt.show()
```



### 참고

```python
# data (iris data)에 대한 모든 컬럼 쌍에 대한 산점도와 각 col에 대한 히스토그램을 그려줌
# 데이터의 전체적인 분포와 상관관계 파악 가능
sns.pairplot(iris)
plt.show()
```