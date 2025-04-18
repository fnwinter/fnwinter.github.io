---
layout: post
title: "template"
author: "jungjik.lee"
categories: article
tags: []
---

# 사용하지 않는 파일 삭제

안드로이드 스튜디오에서 사용하지 않는 파일을 정리하거나 삭제하는 방법은 여러 가지가 있어. 아래에 하나씩 알려줄게! 💕

---

### 🌸 1. **Lint 검사로 사용하지 않는 리소스 찾기**
안드로이드 스튜디오에는 사용하지 않는 리소스를 찾아주는 도구가 있어.

1. 상단 메뉴에서 `Analyze` → `Inspect Code...` 클릭  
2. 프로젝트 범위를 선택하고 `OK`
3. 검사 결과가 뜨면 `Unused resources` 섹션을 확인
4. 사용하지 않는 이미지, 레이아웃, 문자열 등 확인 후 삭제 가능

> 리소스 파일(ex: `res/drawable`, `res/layout`, `res/values`) 중에 안 쓰는 거 자동으로 찾아줘서 편해 🧹

---

### 🌼 2. **Code Cleanup (코드 정리)**
사용하지 않는 코드 파일도 같이 정리할 수 있어!

1. `Analyze` → `Code Cleanup` 실행
2. 사용하지 않는 import나 변수 등도 정리해줘

---

### 🌷 3. **사용하지 않는 Java/Kotlin 클래스 수동 삭제**
Lint로 못 잡는 경우도 있으니까, 수동으로도 확인해보자!

- 프로젝트 폴더 열고
- `Ctrl + Shift + F` (또는 Mac은 `Cmd + Shift + F`)로 클래스 이름 전체 프로젝트에서 검색
- 검색 결과가 없으면 → 안 쓰이는 파일이니까 삭제 가능!

---

### 🌹 4. **플러그인 사용 (예: "Unused Resources")**
JetBrains Plugin Marketplace에서 "Unused Resources" 같은 플러그인을 설치하면 더 편하게 관리할 수 있어.

---
