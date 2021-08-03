---
layout: post
title:  "Multipart/form-data"
description: Django multipart/form-data
date:   2021-08-03 22:12:36 +0530
categories: Django
---

# multipart/form-data
multipart는 MIME type([중요 MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types))이 각각의 파트로 나누어지는 것을 의미하며 request body에 다양한 Content-type을 담을 때 사용한다. 추가적으로 Content-type 필드에 MIME 타입을 기술해줄 수 있는데, 여러 타입중 하나가 **multipart**이다. `request.FILES['키값']`으로 파일들을 통신할 수 있고 `request.POST['키값']` 으로 json 데이터를 통신할 수 있다.

## File upload process

>파일 업로드 구현시, 웹 브라우저 폼을 통해서 파일을 등록하고 전송한다. 웹 브라우저가 보내는 HTTP 메세지는 <br> Content-Type attribute가 multipart/form-data로 지정되며 정해진 형식에 따라 메세지를 인코딩해 전송한다. <br>이를 처리하기 위한 서버는 multipart 메세지에 대해 각 파트별로 분리해 각각의 파일에 대한 정보를 얻는다.

이미지나 음악파일을 첨부해야 할 때 `.jpg` ,`.flac` 파일들이 기존에 다뤘던 데이터들 처럼 파일 자체가 **함께** 전송된다고 생각했다. 이미지나 오디오 파일도 문자로 이루어져 있기 때문에 스팩에 맞게 문자를 생성해 HTTP request body에 담겨져 서버로 보내지게 되는 것이다. 

🚨 내가 생각한 데이터 구조
```
{
    data : [{
            'music_id': [{ "id" : 1,"username" : "ziy0ung" }],
            'album_title': ['안녕안녕'],
            'album_img': [
            	사진이야,
                나도 사진이야
             ]
           },{
            'music_id': [{ "id" : 1,"username" : "ziy0ung" }],
            'album_title': ['하윙하윙'],
            'album_img': [
            	사진2이야,
                나도 사진2이야
             ]
            }
	]
    }
            	
```
💡 진짜로 보내지는 데이터 구조
![](https://images.velog.io/images/ziy0ung1229/post/a5df1abc-5abe-4e5f-8be4-43dc7518b139/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-03%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2012.03.41.png)

통신할 때 json데이터 키값과 파일들을 담고 있는 키값은 따로 전송해야 한다. 그래서 request.body가 아니라 json data는 `request.data`로, 파일은 `request.FIELS['키값']`으로 전달 받을 수 있게 된다.




[참조](https://soooprmx.com/multipart-form-data-%ed%83%80%ec%9e%85%ec%9d%98-http-%eb%a9%94%ec%8b%9c%ec%a7%80-%ea%b5%ac%ec%84%b1-%eb%b0%a9%eb%b2%95/)