---
title: "[Programmers Dev] 수식의 후위 표기법 "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
---

## 스택의 응용 - 수식의 후위 표기법

### 중위 표기법과 후위 표기법

중위 표기법 (infix notation)

: 연산자가 피연산자들의 **사이**에 위치 



> (A + B) * (C + D)



후위 표기법 (postfix notation)

: 연산자가 피연산자들의 **뒤**에 위치

> A B + C D + *



### 중위 표현식 -> 후위 표현식

: **Stack** 을 사용함으로써 연산자들의 우선순위를 지키면서 구현할 수 있다.

- Stack 에는 아직 행하지 않은 연산자들이 들어가게 된다.
- 피연산자는 그냥 출력하고 연산자는 연산자끼리 우선순위를 비교한다.
- Stack 의 top 에 있는 연산자의 우선순위가 높거나 같은결우 pop 을 하고 출력한다.
- top 에 있는 연산자의 우선순위가 낮다면 현재 연산자를 Stack 에 push 한다.

> 1. [중위] A * B + C  	[후위] A B * C +
> 2. [중위] A + B * C      [후위] A B C * +



**1. ** **A * B + C 	->	A B * C +**

(1) 피연산자는 그냥 둔다. -> [A]

(2) 연산자를 만나면 Stack 에 push 한다. -> S = [''*'']

(3) 피연산자는 그냥 둔다. -> [B]

(4) 연산자를 만났지만 Stack 이 비어있지 않으므로 Stack 의 top 과 현재 연산자의

​	 우선순위를 비교한다. -> ''*'' > ''+''

(5) top 위치의 연산자가 우선순위가 높기에 pop 하고 append 한다. -> [A, B, ''*''], S = [ ]

(6) 다음의 연산자를 다시 Stack 에 push 한다. -> [A, B, "*"], S = ["+"]

(7) 피연산자를 만났기에 그냥 둔다. -> [A, B, "*", C]

(8) 수식에 끝까지 왔고 Stack 에 남아있는 것은 아직 행하지 않은 연산이기에

​	 pop 해서 끝에 붙인다. -> [A, B, "*", C, "+"], S = [ ]



**2. A + B * C → A B C * +**

(1) 피연산자는 그냥 둔다. → [A]

(2) 연산자를 만나면 Stack에 push 한다. → S = [''+'']

(3) 피연산자는 그냥 둔다. → [A, B]

(4) 연산자를 만났지만 Stack이 비어있지 않으므로 Stack의 top과 현재 연산자의

​	 우선순위를 비교한다. → "+'' < ''*''

(5) top 위치의 연산자가 우선순위가 낮기에 현재 연산자를 Stack에 push 한다. → S = ["+'',"*"]

(6) 피연산자는 그냥 둔다. → [A, B, C]

(7) 수식에 끝까지 왔으므로 다시 Stack에 들어있는 연산자들을 pop 해서 append한다.

​	  → [A, B, C, ''\*''], S = [''+''] 

​	 → [A, B, C, "*", ''+''] , S = [ ]



### 괄호의 처리

- 여는 괄호를 만나면 stack 에 push 한다.

- 닫는 괄호를 만나면 여는 괄호가 나올 때까지 pop 을 진행한다.

- 연산자를 만났을 때, 여는 괄호 너머까지 pop 하지 않도록 여는 괄호의

   우선순위는 가장 낮게 설정한다.

  -> ex. [중위] A * (B + C)	[후위] A B C + *

**예제**

[중위] (A + B) * (C + D)

[후위] A B + C D + *

1. S = ['( ']
2. S = ['('] , [ A ]
3. S = ['(', '+'], [ A ]
4. S = ['(', '+'], [ A, B]
5. S = [ ], [ A, B, + ]
6. S = ['*'], [A, B, +]
7. S = ['*', '('], [A, B, +]
8. S = ['*', '('], [A, B, +, C]
9. S = ['*', '(', '+'], [A, B, +, C]
10. S = ['*', '(', '+'], [A, B, +, C, D]
11. S = ['*'], [A, B, +, C, D, +]
12. S = [ ], [A, B, +, C, D, +, *]



**연습 문제 - 중위표현 수식 --> 후위표현 수식**

**알고리즘 설계**

- 연산자의 우선순위 설정

- 사칙연산과 소괄호만 사용하는 것을 가정

  > prec = { '*' : 3, '/' : 3, '+' : 2, '-' : 2, '(' : 1 }

- 중위 표현식을 왼쪽부터 한 글자씩 읽어서 
  - 피연산자이면 그냥 출력  
  - '(' 이면 스택에 push 
  - ')' 이면 '('이 나올 때까지 스택에서 pop 한 뒤 출력 
  - 연산자이면 스택에서 이보다 높거나 같은 우선순위 것들을 pop 한 뒤 출력
    - 그리고 이 연산자는 스택에 push 
- 스택에 남아 있는 연산자는 모두 pop 한 뒤 출력



**코드 구현**

```python
class ArrayStack:

    def __init__(self):
        self.data = []

    def size(self):
        return len(self.data)

    def isEmpty(self):
        return self.size() == 0

    def push(self, item):
        self.data.append(item)

    def pop(self):
        return self.data.pop()

    def peek(self):
        return self.data[-1]

prec = {
    '*': 3, '/': 3,
    '+': 2, '-': 2,
    '(': 1
}

def solution(S):
    opStack = ArrayStack()
    answer = ''
    
    for i in S:
        # 연산자이면서 Stack 이 비어있을 때
        if i in prec and opStack.isEmpty(): 
            opStack.push(i)
            
        # 여는 괄호일 때 push    
        elif i =='(': 
            opStack.push(i)
            
        elif i in prec:
            
            # 연산자이면서 top 의 우선순위가 낮을 때 까지 pop
            while not opStack.isEmpty(): 
                
                if prec[opStack.peek()] >= prec[i]:
                    answer += opStack.pop()
                    
                else:
                    break
                    
            opStack.push(i)
            
        # 닫는 괄호일 때 여는 괄호를 만날 때 까지 pop    
        elif i == ')': 
            
            while True:
                t = opStack.pop() 
                
                if t =='(' or opStack.isEmpty():
                    break
                    
                answer += t
                
        # 피연산자가 아닐 경우        
        else: 
            answer += i
            
    # 끝에 왔을 때 Stack에 남아있는 것 출력        
    while not opStack.isEmpty(): 
        answer += opStack.pop()
        
    return answer
```



### 후위 표기 수식 계산

- "-" 이나 "/" 일 경우에는 pop 의 순서가 중요하다.

[후위] A B + C D + *

[전위] (A + B) * (C + D)

1. 피연산자이므로 Stack에 push → S = [ A ]
2. 피연산자이므로 Stack에 push → S = [ A, B ]
3. 연산자를 만났으므로 그 앞에 있던 피연산자 두개를 pop → S = [ ] , [A + B]
4. 피연산자와 연산자 계산 결과를 다시 Stack에 push → S = [ (A + B) ]
5. 피연산자이므로 Stack에 push → S = [ C ]
6. 피연산자이므로 Stack에 push → S = [ D ]
7. 연산자를 만났으므로 그 앞에 있던 피연산자 두개를 pop → S = [ (A + B) ], [C + B]
8. 피연산자와 연산자 계산 결과를 다시 Stack에 push → S = [ (A + B), (C + D) ]
9. 연산자를 만났으므로 그 앞에 있던 피연산자 두개를 pop → S = [ ], [ (A + B), (C + D) ]
10. 피연산자와 연산자 계산 결과를 다시 Stack에 push → S = [ ( (A + B) * (C + D) ]
11. 수식이 끝났으므로 Stack에 남아있는 것을 pop → S = [ ], (A + B) * (C + D)



**알고리즘의 설계**

- 후위 표현식을 왼쪽부터 한 글자씩 읽어서 
  - 피연산자이면 스택에 push
  - 연산자를 만나면 스택에서 pop -> (1), 또 pop -> (2) 로 저장
    - (2) 연산 (1) 을 계산, 이 결과를 스택에 push

- 수식의 끝에 도달하면 스택에서 pop



**코드 구현**

**splitTokens()**

- 수가 들어있으면 이것이 몇 자리 수인지 모르기 때문에 수식이 문자열로 주어졌을 때

  각각을 연산자와 피연산자로 분리해서 리스트로 만드는 함수

```python
def splitTokens(exprStr): # 중위 표현식으로 된 수식 : exprStr
	tokens = [ ]
	val = 0
	valProcessing = False
    
	for c in exprStr:
        
        # 빈칸이면 무시
		if c == ' ': 
			continue
            
        # 숫자를 만나면 여러 숫자로 이루어진 숫자를 10 진수로 만듬    
		if c in '0123456789':
			val = val * 10 + int(c)
            
            # 숫자를 만났다는 것
			valProcessing = True 
            
		else:
            
			if valProcessing:
				tokens.append(val)
				val = 0
			valProcessing = False
			tokens.append(c)
            
	if valProcessing:
		tokens.append(val)
        
	return tokens
```



**infixTopostfix()**

- TokenList 의 순서를 infix 로 부터 postfix 로 변환

```python
def infixToPostfix(tokenList):
    
    prec = {
        '*': 3,
        '/': 3,
        '+': 2,
        '-': 2,
        '(': 1,
    }

    opStack = ArrayStack()
    postfixList = []
    
    for token in tokenList: 
        
        # 피연산자 일 경우
        if type(token) is int: 
            postfixList.append(token)
            
        elif token =='(': # 여는 괄호일 경우
            opStack.push(token)
            
        elif token ==')': # 닫는 괄호일 경우
            
            while True:
                t = opStack.pop()
                if t=='(' or opStack.isEmpty():
                    break
                postfixList.append(t)
                
        # 연산자일 경우        
        else: 
            
            # 연산자이면서 Stack이 비어있을 때
            if opStack.isEmpty(): 
                opStack.push(token)
                
            else:
                # 연산자이면서 top의 우선순위가 낮을 때 까지 pop
                while not opStack.isEmpty():
                    
                    if prec[opStack.peek()] >= prec[token]:
                        postfixList.append(opStack.pop())
                        
                    else:
                        break
                        
                opStack.push(token)  
                
    # 끝에 왔을 때 Stack에 남아있는 것 출력            
    while not opStack.isEmpty(): 
        postfixList.append(opStack.pop())
        
    return postfixList

```



**postfixEval()**

- 후위 표기수식을 계산해서 결과를 리턴하는 함수

```python
def postfixEval(tokenList):
    
    valStack = ArrayStack()
    
    for token in tokenList:
        
        if type(token) is int:
            valStack.push(token)
            
        elif token == '*':
            t1 = valStack.pop()
            t2 = valStack.pop()
            result = t2 * t1
            valStack.push(result)
            
        elif token =='/':
            t1 = valStack.pop()
            t2 = valStack.pop()
            result = t2 / t1
            valStack.push(result)
            
        elif token =='+':
            t1 = valStack.pop()
            t2 = valStack.pop()
            result = t2 + t1
            valStack.push(result)
            
        elif token =='-':
            t1 = valStack.pop()
            t2 = valStack.pop()
            result = t2 - t1
            valStack.push(result)
            
    return valStack.pop()


def solution(expr):
    tokens = splitTokens(expr)
    postfix = infixToPostfix(tokens)
    val = postfixEval(postfix)
    return val

```



## Check Point

- 수식 중위 표기법과 후위 표기법의 차이 알아 두기!
- **stack 응용** 문제 많이 익히기!!

