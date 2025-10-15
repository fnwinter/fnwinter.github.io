---
layout: post
title: "Godot engine folder structure"
author: "jungjik.lee"
categories: article
tags: ["godot", "engine", "overview"]
---

# Godot 엔진 폴더 구조 아키텍처

## 주요 시스템 설명

### 🏗️ **Core 시스템** (파란색)
- **config/**: 프로젝트 설정 및 글로벌 설정
- **crypto/**: 암호화 및 보안 기능
- **debugger/**: 디버깅 시스템
- **input/**: 입력 처리 시스템
- **io/**: 파일 입출력 시스템
- **math/**: 수학 라이브러리 (벡터, 행렬 등)
- **object/**: 객체 시스템 및 메모리 관리
- **os/**: 운영체제 추상화 계층
- **string/**: 문자열 처리 및 국제화
- **variant/**: 동적 타입 시스템

### 🎮 **Drivers 시스템** (보라색)
- **gles3/**: OpenGL ES 3.0 렌더링 드라이버
- **vulkan/**: Vulkan 렌더링 드라이버
- **metal/**: Metal 렌더링 드라이버 (macOS/iOS)
- **d3d12/**: DirectX 12 렌더링 드라이버
- **windows/**: Windows 플랫폼 드라이버
- **unix/**: Unix/Linux 플랫폼 드라이버
- **apple/**: Apple 플랫폼 드라이버

### 🎨 **Editor 시스템** (초록색)
- **gui/**: 에디터 GUI 컴포넌트
- **plugins/**: 에디터 플러그인 시스템
- **import/**: 에셋 임포트 시스템
- **export/**: 게임 내보내기 시스템
- **project_manager/**: 프로젝트 관리자
- **icons/**: 에디터 아이콘 리소스

### 🔧 **Modules 시스템** (주황색)
- **gdscript/**: GDScript 언어 구현
- **mono/**: C# 지원 (Mono)
- **godot_physics_2d/**: 2D 물리 엔진
- **godot_physics_3d/**: 3D 물리 엔진
- **jolt_physics/**: Jolt 물리 엔진
- **navigation_2d/**: 2D 네비게이션
- **navigation_3d/**: 3D 네비게이션
- **multiplayer/**: 멀티플레이어 네트워킹
- **webrtc/**: WebRTC 지원
- **websocket/**: WebSocket 지원

### 🌐 **Platform 시스템** (분홍색)
- **windows/**: Windows 플랫폼 지원
- **linuxbsd/**: Linux/BSD 플랫폼 지원
- **macos/**: macOS 플랫폼 지원
- **android/**: Android 플랫폼 지원
- **ios/**: iOS 플랫폼 지원
- **web/**: 웹 플랫폼 지원 (WebAssembly)
- **visionos/**: VisionOS 플랫폼 지원

### 🎭 **Scene 시스템** (연두색)
- **2d/**: 2D 씬 노드들
- **3d/**: 3D 씬 노드들
- **gui/**: GUI 노드들
- **animation/**: 애니메이션 시스템
- **audio/**: 오디오 노드들
- **resources/**: 리소스 시스템
- **main/**: 메인 씬 관리

### ⚙️ **Servers 시스템** (청록색)
- **rendering/**: 렌더링 서버
- **audio/**: 오디오 서버
- **physics_server_2d.cpp**: 2D 물리 서버
- **physics_server_3d.cpp**: 3D 물리 서버
- **navigation_server_2d.cpp**: 2D 네비게이션 서버
- **navigation_server_3d.cpp**: 3D 네비게이션 서버
- **text_server.cpp**: 텍스트 렌더링 서버
- **display_server.cpp**: 디스플레이 서버

## 아키텍처 특징

1. **모듈화된 설계**: 각 시스템이 독립적인 모듈로 구성
2. **플랫폼 독립성**: 플랫폼별 드라이버로 크로스 플랫폼 지원
3. **서버 기반 아키텍처**: 핵심 기능들이 서버로 구현되어 느슨한 결합
4. **확장 가능성**: 플러그인 시스템과 모듈 시스템으로 확장 가능
5. **계층화된 구조**: Core → Drivers → Servers → Scene → Editor 순서로 계층화
