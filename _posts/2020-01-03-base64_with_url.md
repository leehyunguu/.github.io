---
title: "Base64로 구성된 URL 호출 시 주의사항"
date: 2020-01-03
categories: diary Base64 URL 
---
버그 발생!

URL에 Base64 인코딩된 String을 포함하여 Query String을 구성하여 보내는 과정에서 문제가 발생했다.

[이 글]을 보면 알겠지만, Base64의 경우 특수문자가 "/", "+"이렇게 두개가 들어간다.

그런데 Query String을 "+"를 공백문자로 처리해버리기 떄문에 문제가 발생한것.

검색 후에 확인한 처리 방법은 두가지 정도가 있다.

1. Encoding을 할때 [URLEncoder]를 통해서 Encoding후 보내고, Decoding할 때 [URLDecoder]를 통해서 Decoding를 하는 방법
2. Base64로 변환할 때 [Base64.encodeBase64URLSafeString]을 통해 URL Safe한 Encoding을 하고, [Base64.decodeBase64]를 통해 Decoding을 하는 방법

URL에 특수문자가 포함 될 경우 어떤예외상황이 나타나는지 확인하고 개발해야겠다..

[이 글]: https://ko.wikipedia.org/wiki/%EB%B2%A0%EC%9D%B4%EC%8A%A464
[URLEncoder]: https://docs.oracle.com/javase/8/docs/api/java/net/URLEncoder.html
[URLDecoder]: https://docs.oracle.com/javase/8/docs/api/java/net/URLDecoder.html
[Base64.encodeBase64URLSafeString]: http://commons.apache.org/proper/commons-codec/apidocs/org/apache/commons/codec/binary/Base64.html#encodeBase64String-byte:A-
[Base64.decodeBase64]: http://commons.apache.org/proper/commons-codec/apidocs/org/apache/commons/codec/binary/Base64.html#decodeBase64-java.lang.String-
