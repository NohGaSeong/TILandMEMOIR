# Python 문법 정리
## 시작하기 앞서
- 파이썬을 알고있긴 하지만 정확히 기억이 안나 다시 정리를 해본다.
- 이 파이썬이라는 언어가 어떻게 태어났고 어떠한 장단점이 있는지는 따로 서술하지 않아도 될 듯 싶어 바로 본론으로 들어가겠다.

## Hello Wolrd
- `pirnt("Hello World")` 라고 작성하면되는 아주 쉬운 언어이다.
- 굳이 설명하자면 print() 함수에 문자열을 집어넣어서 출력 시킨겁니다.

## 연산, 변수
### 연산
- 연산이 가능합니다. `+` , `-`, `/` , `*`, `%` (순서대로 더하기,빼기,나누기,곱하기,나머지 연산자)
### 변수
- 어떤 데이터를 저장하고, 이를 자유롭게 처리하는 것.
```.py
a = 10
print(a)

## 결과 : 10
## 이런식으로 하면 a의 값이 출력된다

b = 30

sum = a+b

print(sum)

## 을 하게 된다면 a+b인 40이 출력된다.
```
- 변수에는 정수뿐만 아니라 실수나 문자도 넣어줄 수 있다.
```.py
name = 'Gaseong'
city = 'Seoul'
a = 10.5
## 이런식으로 말이다
```
- 참과 거짓을 나타내는 변수도 있다.
```
live_in_seoul = False
live_in_Gwangu = True
```

## 리스트
- C언어의 배열이라고 생각하면 편하다. 많은 데이터를 한꺼번에 다루기 위해 리스트를 사용한다.
```.py
grade = ['A','B','C']
print(grade[0]) #을 하면 A가 출력된다. 리스트의 값은 0부터 시작한다.

odd_number = [1,3,5,7,9]
print(odd_number) #을 하면 리스트가 다 출력된다. 

user_data = [20, 'Gaseong', 'Seoul', False] #처럼 다양한 종류의 변수들을 섞어 쓸 수 있다. 
```
## 사전(딕셔너리)
- `키` 를 써서 데이터를 접근하고 사용한다.
```.py
# 딕셔너리를 쓰기 위해선 아래와 같이 변수 = {} 을 적어줘야한다. 이 코드에선 'age'와 'address'가 키로 쓰였다.
user = {}
user['age'] = 25
user['address'] = 'seoul'

print(user)

# 딕셔너리에서 값을 가져오는 방식 2개. .get 을 쓰는걸 권장한다.(키가 없어도 에러가 생기지 않기 때문)
print(user['age'])
print(user.get('age'))
```

## 조건문
- 말그대로 조건을 걸어주는겁니다. 
```.py
live_in_seoul = False

if live_in_seoul == Ture:
  print('서울에 산다.')
  
elif live_int seoul == False:
  print('서울에 살지 않는다.')
```

## 조건문 For문
- 리스트가 많을때 for을 써서 반복적인 작업으로 처리하면됩니다.
```.py
odd_number = [1,3,5,7,9,11]

for num in odd_number: #num 은 odd_number에 있는 변수이다. 
  print(odd_number] # 이러면 리스트 안에 있는 숫자들이 전부 출력됩니다.
```
- for문은 if문과 함께 쓰이는 경우가 많은데 한번 짝수만 출력하는 함수를 만들어봅시다.
```.py
number = [1,2,3,4,5,6,7]

for num in number:
  if num % 2 == 0:
    print(num)
    # 이러면 num을 2로 나눴을때 나머지가 0인 짝수들만 출력되게됩니다.    
```
- for 문은 실행중에도 멈출 수 있습니다. `break` 라는 친구를 써주면 돼요
```.py
ages = [10,20,30,40,50,60]
for i in ages :
  if i > 30:
    print('여기서 스톱')
    break
```

## 함수
- 같은 일을 반복하지 않기 위해 사용합니다. 
- 더하기를 예시로 들자면 계속 더하기 귀찮잖아요 변수가 여러개일때? 이때 함수를 만드는겁니다.
- 함수 앞엔 항상 def 를 적어줭햐ㅏㅂ니다.
```.py
def add(x,y,z): #add 함수. x,y,z 는 입력값
  return x+y+z # 함수 내에서 계산을 하고 함수 밖으로 내보냅니다.
  
result = add(10,30,50)
print(result) #하면 저 숫자들이 더해져서 출력됩니다.
```
### 파이썬 내장 함수
```
a = "Good morning, man"
a.upper() # - 대문자로 바꿔줍니다.



a.lower() #  소문자로 바꿔줍니다.
a.count('m') # m이 몇개나 있는지 세줍니다.


a = "Life is too short"
a.replace("Life", "Your height")


a = "I regret what I did to you"
a.split()  # split은 문자열을 나누는 함수다.  값을 넣지 않으면 공백으로 잘라줍니다
['I', 'regret', 'what', 'I', 'did', 'to', 'you']

d = "home,mother,sweet"
d.split(",")
['home', 'mother', 'sweet']


a.swapcase() # 대문자와 소문자를 바꾸어준다.


str(3) # str은 문자열로 만들어주는 함수이다. str(3)을 실행하면 문자열이 된다.

len("hi") # 길이를 알려주는 함수이다.
```

## 여기까지 알아보자
- 여기까지 알아봤으면 기본 문법은 땐것같고... Django 의 문법? 이라해야하나. 그런것들이나 배우러가봅시다. 아자!
