---
title: Jetbrain IDE 에서 Replace All 할 때 짧은 팁
date: 2020-09-22
categories: jetbrain
---
현재 블로그 글을 Rubymine으로 작성하고 있다.

이번에 카테고리 정리를 하면서 diary 카테고리에 다른 카테고리가 더 있는 글들을 diary 하나만으로 변경하기 위해

Replace All을 사용했다.

먼저 카테고리가 diary인 글들을 찾기 위해 <code>Ctrl+Shift+R</code>로 모든 글 중에 <code>categories: diary</code>가 포함된 줄을 찾았다.

그다음 검색 조건에 regex를 켜주고, <code>categories: diary .*</code>라고 검색하면 카테고리에 추가로 붙은 내용까지 모두 선택이 된다.

그 후 <code>categories: diary</code>로 Replace All을 해주면 된다.

이렇게 Regex를 이용해 뒤에 추가로 분터있는 글자들을 모두 없앨 수 있다.
