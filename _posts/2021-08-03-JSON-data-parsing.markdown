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