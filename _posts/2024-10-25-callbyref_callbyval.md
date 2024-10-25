---
title: Call by ref vs Call by val 
date: 2024-10-25 00:00:00 +0900
author: JunHyeokDev
categories: [Jungle Keyword, OS]
tags: [Study]
---

## 1. Call by Value (값에 의한 호출)
```python
def modify_value(x):
    print(f"함수 내부 처음 x의 id: {id(x)}")
    x = 100  # 새로운 객체를 참조하게 됨
    print(f"함수 내부에서 x 수정 후의 id: {id(x)}")

# 테스트
number = 42
print(f"함수 호출 전 number의 id: {id(number)}")
modify_value(number)
print(f"함수 호출 후 number: {number}")  # 42 출력
print(f"함수 호출 후 number의 id: {id(number)}")
```

### 특징
- 매개변수로 전달될 때 값이 복사되어 전달됨
- 함수 내부에서 매개변수를 변경해도 원본 값은 변경되지 않음
- 파이썬에서 int, float, str, tuple 등 불변 객체에 대해 이러한 동작을 보임

## 2. Call by Reference (참조에 의한 호출)
```python
def modify_list(lst):
    print(f"함수 내부 처음 lst의 id: {id(lst)}")
    lst.append(4)  # 객체 내용 수정
    print(f"함수 내부에서 수정 후 lst의 id: {id(lst)}")

# 테스트
numbers = [1, 2, 3]
print(f"함수 호출 전 numbers의 id: {id(numbers)}")
modify_list(numbers)
print(f"함수 호출 후 numbers: {numbers}")  # [1, 2, 3, 4] 출력
print(f"함수 호출 후 numbers의 id: {id(numbers)}")
```

### 특징
- 매개변수로 객체의 주소값이 전달됨
- 함수 내부에서 객체를 수정하면 원본 객체도 함께 변경됨
- 파이썬에서 list, dict, set 등 가변 객체에 대해 이러한 동작을 보임

## 3. 주의해야 할 점

### 불변 객체의 재할당
```python
def modify_tuple(t):
    print(f"함수 내부 처음 t의 id: {id(t)}")
    t = t + (4,)  # 새로운 튜플 객체 생성
    print(f"함수 내부에서 수정 후 t의 id: {id(t)}")

# 테스트
numbers = (1, 2, 3)
print(f"함수 호출 전 numbers의 id: {id(numbers)}")
modify_tuple(numbers)
print(f"함수 호출 후 numbers: {numbers}")  # (1, 2, 3) 출력
print(f"함수 호출 후 numbers의 id: {id(numbers)}")
```

### 가변 객체 내부의 불변 객체
```python
def modify_mixed_list(lst):
    lst[0] = 100  # 리스트 내부의 요소 변경

# 테스트
numbers = [1, "hello", [1, 2, 3]]
modify_mixed_list(numbers)
print(numbers)  # [100, "hello", [1, 2, 3]] 출력
```

## 4. 요약
- **Call by Value (값 전달)**: 
  - 불변 객체에 대한 연산
  - 원본 값 보존
  - 새로운 객체 생성
  
- **Call by Reference (참조 전달)**:
  - 가변 객체에 대한 연산
  - 원본 객체 수정 가능
  - 동일한 객체 참조 유지

## 5. 팁
```python
# id() 함수를 사용하여 객체의 메모리 주소 확인
x = [1, 2, 3]
y = x
print(id(x) == id(y))  # True: 같은 객체를 참조

# is 연산자를 사용하여 객체 동일성 검사
print(x is y)  # True: 같은 객체를 참조
```

