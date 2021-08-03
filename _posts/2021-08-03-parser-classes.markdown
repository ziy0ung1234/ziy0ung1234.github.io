---
layout: post
title:  "parser_classes"
description: DRF_parser_classes
date:   2021-08-03 22:27:40 +0530
categories: Django Python DRF parser
---

✨  본 글은 [DRF 공식문서](https://www.django-rest-framework.org/api-guide/parsers/)를 바탕으로 작성하였습니다.
# Parser
파서(parser)란 파싱을 수행하는 프로그램을 의미하며 Django REST Framework는 다양한 미디어 유형의 request들을 승인할 수 있는 많은 내부 parser class들을 지원한다. 또한 우리가 파서를 정의하고 커스텀해서 사용할 수도 있어 API가 허용하는 미디어 유형들을 유연하게 다룰 수 있다.

## DRF Parser class

### JSONParser
- 들어오는 `json` 컨텐츠 리퀘스트를 파이썬 컨텐츠 유형인 `dict`로 파싱한다.
- `Content-Type`이 `application/json`으로 설정된 경우에 사용

### FormParser
- `HTML` 양식의 content를 파싱. 
- `request.data`를 찍어보면 데이터가 `QueryDict`으로 출력
- `Content-Type`이 `application/x-www-form-urlencoded`로 설정된 경우에 사용

### MultiPartParser
- 파일 업로드를 지원하는 `multipart HTML` 양식의 content를 파싱.
- `request.data`를 찍어보면 데이터가 `QueryDict`으로 출력
- FormParser와 MultiPartParser는 HTML 양식의 데이터를 완전히 서포트 하기 위해 함께 사용한다.
- `Content-Type`이 `multipart/form-data`로 설정된 경우에 사용


## How to use the parser class
파일과 관련JSON들을 업로드 해야할 때 MultiPartParser를 사용한다. parser class는  serializer나 models가 아니라 요청을 수신하고 처리하는 역할을 하는 View에서 사용한다. 클래스 기반 뷰에서 parser_classes 속성을 사용해 파서를 정의한다.

```py
class UserUploadedPicture(APIView):
    parser_classes = (MultiPartParser, )
    
    def post(self, request, format=None):
    	~~블라블라~~
        return JsonResponse(serializer.errors, status=400)
```