---
layout: post
title: "template"
author: "jungjik.lee"
categories: article
tags: [android, test]
---

# Android Test

안드로이드에서 크롬 브라우저를 사용해 `/sdcard/data/index.html` 파일을 여는 ADB 명령어는 아래와 같이 입력할 수 있어:

```bash
adb shell am start -a android.intent.action.VIEW -d "file:///sdcard/data/index.html" -n com.android.chrome/com.google.android.apps.chrome.Main
```

### 설명:
- `adb shell am start`: 액티비티 실행 명령
- `-a android.intent.action.VIEW`: 파일을 보기 위한 인텐트
- `-d "file:///sdcard/data/index.html"`: 파일 경로 (파일 URL 스킴 사용)
- `-n com.android.chrome/com.google.android.apps.chrome.Main`: 크롬 브라우저를 지정

---

하지만 중요한 점은 **Chrome에서는 보안상의 이유로 `file://` 경로를 기본적으로 차단**하고 있어서, 직접 열 수 없을 수도 있어.  
이럴 경우 아래 두 가지 대안을 추천해:

---

### 💡 대안 1: 파일을 웹 서버에 올리고 http:// 주소로 접근
1. `adb forward tcp:8000 tcp:8000`
2. PC에서 `python3 -m http.server 8000` 등으로 간단한 웹서버 실행
3. 크롬에서 `http://127.0.0.1:8000/data/index.html` 로 접근

---


### 📌 설치해야 할 라이브러리:
```bash
pip install pillow numpy
```

### 🐍 파이썬 이미지 비교 스크립트:
```python
from PIL import Image, ImageChops
import numpy as np

def compare_images(img_path1, img_path2, diff_output_path=None):
    # 이미지 열기
    img1 = Image.open(img_path1).convert('RGB')
    img2 = Image.open(img_path2).convert('RGB')

    # 이미지 크기 같게 맞추기
    if img1.size != img2.size:
        print("이미지 크기가 다릅니다. 비교하려면 같은 크기여야 해요!")
        return

    # 픽셀 단위로 차이 계산
    diff = ImageChops.difference(img1, img2)

    # numpy 배열로 변환해서 차이 비율 계산
    diff_np = np.array(diff)
    diff_pixels = np.count_nonzero(diff_np)
    total_pixels = diff_np.size

    diff_ratio = diff_pixels / total_pixels * 100
    print(f"다른 픽셀 비율: {diff_ratio:.2f}%")

    # 차이 이미지 저장하기 (선택)
    if diff_output_path:
        diff.save(diff_output_path)
        print(f"차이 이미지를 저장했어요: {diff_output_path}")

# 사용 예시
compare_images("image1.png", "image2.png", "diff_output.png")
```

### 💡 설명:
- `ImageChops.difference()`는 두 이미지의 픽셀 간 차이를 계산해줘.
- 차이를 시각적으로 보고 싶을 땐 `diff_output_path`에 저장하면 돼.
- 픽셀 값이 완전히 똑같지 않으면 다른 것으로 간주해. (완벽 비교)

혹시 비교 허용 오차(예: 약간 흐릿하거나 압축된 이미지)도 포함하고 싶으면 말해줘~ 좀 더 부드러운 비교 버전도 만들어줄 수 있어! 😘

오키오키~ 😘 너가 말한 건, **APK를 실제 Android 기기에 설치한 후**, **실행 가능한(런처에서 실행할 수 있는) Activity**를 찾고 싶다는 거지?

그럴 땐 **ADB 명령어**로 기기 안에 설치된 앱의 **런처 액티비티**를 찾을 수 있어! 아래 단계대로 따라 해봐 💁‍♀️

---
# 실행 가능한 apk 찾기

### ✅ 1. APK 설치하기
```bash
adb install your_app.apk
```

---

### ✅ 2. 패키지 이름 확인하기
APK 설치 후 패키지 이름을 모르면 다음 명령어로 확인할 수 있어:

```bash
adb shell pm list packages | grep your_app_name
```

예:  
```bash
adb shell pm list packages | grep example
# 결과: package:com.example.myapp
```

---

### ✅ 3. 실행 가능한 (런처) Activity 찾기

```bash
adb shell cmd package resolve-activity --brief com.example.myapp | tail -n 1
```

예:
```bash
adb shell cmd package resolve-activity --brief com.example.myapp | tail -n 1
# 결과: com.example.myapp/.MainActivity
```

이게 **런처에서 실행 가능한 메인 액티비티**야!

---

### ✅ 4. 수동 실행 테스트 (실행 가능한지 확인하고 싶다면)
```bash
adb shell am start -n com.example.myapp/.MainActivity
```

---

### 💡 추가 팁: 모든 액티비티 확인
```bash
adb shell dumpsys package com.example.myapp | grep -A 10 "Activity Resolver Table:"
```

여기엔 등록된 모든 Activity들과 관련된 인텐트 필터 정보가 나와. 좀 복잡하지만, `MAIN`, `LAUNCHER` 인텐트가 설정된 걸 찾으면 돼!
