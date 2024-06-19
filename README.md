#[ 10주차 미션 제출 ]

#1) 프로젝트의 주제 : 경기도 지역 기온과 사망자의 상관관계 분석  :  그래프로는 정확히 상관관계가 분석되지 않아 10년간의 월별 사망자의 합계를 구해보니 경기도 수원 지역에서는 7월, 9월, 11월 순으로 가장 많은 사망자가 발생하였다. 뚜렷한 기온과의 상관관계를 찾아 내지는 못했다.

#2) 프로젝트 코랩 링크:https://colab.research.google.com/drive/1c904Nf74vItGBXNJwo5N0K5wHkbHTEBA?usp=sharing

#3) 깃헙 링크 : https://github.com/leenamhee7937/project10/blob/main/README.md

from google.colab import files
files.upload()

# 도시 이름을 입력 받아 2014년도~2023년도의 경기도 사망자 월별자료
# 2014년도~2023년도의 관측지 경기도 수원 월별 기온 (월(2014-01), 평균기온, 최저기온, 최고기온)
import csv
data1 = csv.reader(open('dead13.csv'))
data2 = csv.reader(open('temp14.csv'))
d = [0]*121
t = []
m = []

name = input('경기도 도시 이름을 입력하세요:')
for row in data1 :
  if name in row[0] :
    for i in range(1, 121) :
      d[i] = d[i] + int(row[i])

for i in range(0, 120) :
  d[i] = d[i+1]
del d[120]

next(data2)
for row in data2 :
 t.append(float(row[1])*15)   # 그래프 구간이 너무 차이가 나서 온도에 15를 곱한 갑으로 그래프를 그려봄.
 m.append(row[0][-4:])

a = [0]*12
for k in range(0, 12):           # 그래프로 잘 구분이 안되어 10년간 월별 사망자수의 합계를 구해봄.
  for i in range(k, 120, 12) :
     a[k] = a[k] + d[i]

print(a)

print(d)
print(t)
print(m)

import matplotlib.pyplot as plt
plt.figure(figsize=(20, 6))
plt.plot(m, d, label='dead')
plt.plot(m, t, label='temp')
plt.legend()
plt.show()
