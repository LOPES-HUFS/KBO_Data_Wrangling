# Pandas를 이용해 KBO data 살펴보기

필요한 것들 import

```python
import pandas as pd
```

## 팀 자료 살펴 보기

전제 스코어 자료 불러오기

```python
scoreboard = pd.read_csv("./sample/scoreboard.csv")
```

한화 승패 가져오기

```python
sum(scoreboard[(scoreboard['팀'] == "한화")&(scoreboard['year'] == 2019)]["승패"] == "승")

win = []
loss = []

for i in range(2010, 2021):
    temp_win = sum(scoreboard[(scoreboard['팀'] == "한화")&(scoreboard['year'] == i)]["승패"] == "승")
    temp_loss = sum(scoreboard[(scoreboard['팀'] == "한화")&(scoreboard['year'] == i)]["승패"] == "패")
    win.append(temp_win)
    loss.append(temp_loss)

win, loss
```

## 그래프 그리기

```python
import matplotlib.pyplot as plt
%matplotlib inline
```

한화 승패 그래프 그리기

```python

hanhwa = {"win": win, "loss": lose}
hanhwa = pd.DataFrame(hanhwa, index=list(range(2010, 2021)))

hanhwa.plot();
```

두산 에러 그래프 그리기

```python
team = []

for i in range(2010, 2021):
    temp = sum(scoreboard[(scoreboard['팀'] == "두산")&(scoreboard['year'] == i)]["E"])
    team.append(temp)

team = pd.Series(team, index=list(range(2010, 2021)))

team.plot();
```

두산, 한화, LG 에러 그래프 함께 그리기

```python

team_1 = []
team_2 = []
team_3 = []

for i in range(2010, 2021):
    temp = sum(scoreboard[(scoreboard['팀'] == "두산")&(scoreboard['year'] == i)]["E"])
    team_1.append(temp)
    temp = sum(scoreboard[(scoreboard['팀'] == "한화")&(scoreboard['year'] == i)]["E"])
    team_2.append(temp)
    temp = sum(scoreboard[(scoreboard['팀'] == "LG")&(scoreboard['year'] == i)]["E"])
    team_3.append(temp)

#team_1, team_2, team_3

teams = {"Dusan": team_1, "hanhwa": team_2, "LG": team_3}
teams = pd.DataFrame(teams, index=list(range(2010, 2021)))

#teams

teams.plot();
```
