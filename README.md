#[ 10주차 미션 제출 ]

#1) 프로젝트의 주제 : 경기도 지역 기온과 사망자의 상관관계 분석  : 그래프로는 정확히 구분되지 않아 10년간의 월별 사망자의 합계를 구해보니 경기도 대부분의 지역에서 1월에 가장 많은 사망자가 발생하였다.
                                                                  가장 추운 계절에 많은 사망자 수가 발생하는 것을 분석할 수 있었다.

#2) 프로젝트 코랩 링크:https://colab.research.google.com/drive/1c904Nf74vItGBXNJwo5N0K5wHkbHTEBA?usp=sharing

#3) 깃헙 링크 : https://github.com/leenamhee7937/project10/blob/main/README.md

from google.colab import files
files.upload()

# 도시 이름을 입력 받아 2014년도~2023년도의 경기도 사망자 월별자료
# 2014년도~2023년도의 관측지 경기도 수원 월별 기온 (월(2014-01), 평균기온, 최저기온, 최고기온)
import csv
data1 = csv.reader(open('dead14.csv'))
data2 = csv.reader(open('temp14.csv'))
d = []
t = []
m = []

name = input('경기도 도시 이름을 입력하세요:')
for row in data1 :
  if name in row[0] :
    for i in range(2, 122) :
      d.append(int(row[i]))
    break


next(data2)
for row in data2 :
 t.append(float(row[3])+50)
 m.append(row[0])

print(d)
print(t)
print(m)

import matplotlib.pyplot as plt
plt.figure(figsize=(20, 6))
plt.plot(m, d, label='dead')
plt.plot(m, t, label='temp')
plt.legend()
plt.show()
