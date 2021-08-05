---
layout: post
title:  "JSON data parsing"
description: Python_JSON data parsing
date:   2021-08-03 22:21:40 +0530
categories: Django Python 
---


 - 웹 언어인 Javascript의 데이터 객체를 표현하는 방식/언어
 - 간결하다는 장점이 있어 기계,인간 모두가 이해하기 쉬움
 - 경량의 데이터 교환 형식, 단순히 데이터를 표시하는 표현방법
 
```
 {
  "employees": [
    {
      "name": "ziy0ung",
      "lastName": "Han"
    },
    {
      "name": "jiyoung",
      "lastName": "Kim"
    },
    {
      "name": "ddiy0ung",
      "lastName": "Park"
    } 
  ]
}
```

## JSON(JavaScript Object Notation) 형식
### 1. name-value 형식의 쌍
- 다양한 언어들에서 object, hashtable, struct로 실현되었다.

`{ String key : String value }`

```
{
  "firstName": "ziy0ung",
  "lastName": "Han",
  "email": "dnjsejrjfsm1@gmail.com"
}
```
_💡**value**에 들어갈 수 있는 자료형 : Number, String, Boolean, Array, Object, Null,,💡_
### 2. 값들의 순서화 된 리스트 형식
- 다양한 언어들에서 array, list로 실현되었다.

`[ value1, value2, ….. ]`

```
{
  "firstName": "ziy0ung",
  "lastName": "Han",
  "email": "dnjsejrjfsm1@gmail.com",
  "hobby": ["listening music","watching movies"]
}
```
[참조1](https://nesoy.github.io/articles/2017-02/JSON)
[참조2](https://velog.io/@ym1085/JSON-%EC%82%AC%EC%9A%A9%EB%B2%95)
# parsing
 컴퓨터 분야에서 `JSON` , `XML` , `HTML` 등으로 구성된 데이터를 분석하여 내가 원하는 부분만 추출하고자 하는 것
 
[참조](https://www.opentutorials.org/course/3718/25092)
 
## json.loads
`json.loads`는 JSON 데이터를 파이썬으로 디코딩 하는 중요 메서드로 아래 변환표처럼 s(JSON 문서를 포함하는 **str** , **bytes** , **bytearray** 인스턴스)를 파이썬 객체로 역직렬화(deserialize)한다.

### 변환표

| JSON | Python |
|:----------|:----------:|
| 오브젝트(object)| dict|
| 배열(array)| list|
| 문자열(string)| str|
| 숫자(정수)| int|
| 숫자(실수)| float|
| true| True|
| false| False|
| null| None|

[참조](https://docs.python.org/ko/3/library/json.html#json-to-py-table)

디코드 할때 역직렬화되는 데이터가 유효한 JSON 문서가 아닐 경우에는, `JSONDecodeError`가 발생하기 때문에 에러 핸들링을 해주어야 한다.

## JSON(JavaScript Object Notation) 파싱

### 1. Key:Value(1)
```py
import json

music_id = '{"id":1,"username":"ziy0ung","display_name":"ziy0ung"}'
jsonObject = json.loads(music_id)
print(jsonObject['display_name']) 	# ziy0ung
print(type(jsonObject))			# <class 'dict'>
```
 
 ### 2. Key:Value(N)
 ```py
 import json

music_id   = '{"id":1,"username":"ziy0ung","display_name":["ziy0ung", "jiy0ung"]}'
jsonObject = json.loads(music_id)
jsonArray  = jsonObject['display_name']
for name in jsonArray:
	print(name)
------------------------------------------------------------    
#ziy0ung
#jiy0ung
```

### 3. key:Value(object)
```py
import json

music_id   = '{"id":1,"username":"ziy0ung","display_name":{"korean":"지영", "english":"jiyoung"}}'
jsonObject = json.loads(music_id)
print(jsonObject['display_name']["korean"])	# 지영

```
### 4. key:value([object])

```py
import json

music_id   = '{"id":1,"username":"ziy0ung","display_name":[{"korean":"지영", "english":"jiyoung"},{"korean": "띠옹", "english": "DDiong"}]}'
jsonObject = json.loads(music_id)
jsonArray  = jsonObject['display_name']
for name in jsonArray:
	print(name['korean'])
------------------------------------------------------------
# 지영
# 띠옹
```