# AURA

<img width="1491" height="1055" alt="image" src="https://github.com/user-attachments/assets/1658567b-ff8b-45f9-8f97-51a32e348482" />


> Gmail과 Google Drive에 쌓인 유령 데이터를 찾아, 사용자가 직접 확인하고 안전하게 정리할 수 있도록 돕는 서비스
> 

AURA는 사용자의 Gmail과 Google Drive에 저장된 오래된 메일, 광고성 메일, 중복 파일, 오래된 Drive 파일, 대용량 파일을 분석해 정리 후보로 제안하는 클라우드 데이터 정리 서비스입니다.

사용자는 Google 계정을 연결한 뒤 스캔 조건을 설정하고, AURA는 메일과 파일의 원문 전체가 아닌 제한된 메타데이터를 기반으로 AI 의미 분석을 수행합니다. 분석 결과는 Spring Boot 서버의 Decision Engine을 거쳐 정리 후보와 보호 대상으로 분류되며, 최종 휴지통 이동은 사용자가 승인한 항목에 대해서만 실행됩니다.

---

## 01. Problem & Solution

### Problem

Gmail과 Google Drive는 오래 사용할수록 광고성 메일, 오래된 첨부 메일, 중복 파일, 임시 백업 파일, 대용량 자료가 계속 쌓이기 쉽습니다.

하지만 사용자가 직접 모든 메일과 파일을 확인하며 정리하기는 번거롭고, 중요한 영수증, 계약서, 공유 문서까지 실수로 삭제할 위험도 있습니다. 또한 방치된 클라우드 데이터는 저장 공간 낭비뿐 아니라 디지털 탄소 배출 문제와도 연결됩니다.

### Solution

AURA는 Gmail과 Google Drive의 메타데이터를 수집하고, Gemini API 기반 의미 분석과 Spring Boot Decision Engine을 결합해 정리 후보를 제안합니다.

사용자는 광고, 수업, 영수증처럼 직접 입력한 키워드와 기간, 파일 조건을 기준으로 개인화된 후보를 확인할 수 있습니다. AURA는 최종 삭제를 자동으로 수행하지 않고, 사용자의 명시적 승인 이후에만 Gmail 또는 Drive의 휴지통으로 항목을 이동합니다.

---

## 02. Tech Stack

### Frontend

![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge\&logo=react\&logoColor=61DAFB)
![Expo](https://img.shields.io/badge/Expo-000020?style=for-the-badge\&logo=expo\&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge\&logo=react\&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge\&logo=typescript\&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white)

### Backend

![Java 21](https://img.shields.io/badge/Java_21-007396?style=for-the-badge\&logo=openjdk\&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge\&logo=springboot\&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge\&logo=springsecurity\&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge\&logo=jsonwebtokens\&logoColor=white)
![JPA](https://img.shields.io/badge/JPA-59666C?style=for-the-badge)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge\&logo=swagger\&logoColor=black)

### AI, Database & Infra
![Codex](https://img.shields.io/badge/opencode-%23000000.svg?style=for-the-badge&logo=opencode&logoColor=ffffff)
![Gemini API](https://img.shields.io/badge/google%20gemini-%238E75B2.svg?style=for-the-badge&logo=google%20gemini&logoColor=white)
![Google Cloud](https://img.shields.io/badge/GoogleCloud-%234285F4.svg?style=for-the-badge&logo=google-cloud&logoColor=white)
![Gmail](https://img.shields.io/badge/Gmail-%23D14836.svg?style=for-the-badge&logo=gmail&logoColor=white)
![Google Drive](https://img.shields.io/badge/Google%20Drive-%234285F4.svg?style=for-the-badge&logo=googledrive&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge\&logo=mysql\&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Amazon%20EC2-FF9900?style=for-the-badge&logo=Amazon%20EC2&logoColor=white)
![Firebase FCM](https://img.shields.io/badge/Firebase_FCM-FFCA28?style=for-the-badge\&logo=firebase\&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge\&logo=nginx\&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge\&logo=githubactions\&logoColor=white)

---

## 03. Main Features

### Google 계정 로그인 및 권한 연결

Google OAuth 2.0을 통해 사용자를 인증하고, Gmail과 Google Drive 접근 권한을 서비스에 필요한 범위로 연결합니다. 사용자는 설정 화면에서 권한 상태를 확인하거나 다시 연결할 수 있습니다.

### Gmail 및 Drive 메타데이터 스캔

Gmail API와 Google Drive API를 통해 메일 제목, 발신자 도메인, 라벨, 스니펫 일부, 파일명, 경로, MIME 타입, 크기, 생성일, 수정일, 마지막 열람일 같은 메타데이터를 수집합니다.

### Gemini API 기반 AI 의미 분석

사용자가 입력한 포함 키워드와 제외 키워드를 기준으로 메일과 파일의 의미를 분석합니다. 예를 들어 `수업`, `광고`, `영수증`처럼 넓은 의미의 키워드도 제목, 폴더 경로, 라벨, 스니펫 일부를 함께 고려해 관련성을 추론합니다.

### Decision Engine 기반 후보 확정

Gemini 응답을 그대로 삭제 후보로 사용하지 않고, Spring Boot 내부 Decision Engine이 보호 규칙, 중복 탐지, 기간 조건, 사용자 키워드 조건을 검증해 최종 정리 후보와 보호 대상을 결정합니다.

### 사용자 승인 기반 휴지통 이동

AURA는 자동 삭제를 수행하지 않습니다. 사용자가 앱에서 후보를 확인하고 최종 승인한 항목만 Gmail 또는 Google Drive 휴지통으로 이동합니다.

### 저장소 및 휴지통 관리

사용자는 저장된 메일과 Drive 파일을 확인하고, 휴지통으로 이동된 항목을 복구하거나 별도 확인 절차를 거쳐 영구 삭제할 수 있습니다.

### 탄소 절감 통계

정리한 데이터 용량을 기반으로 예상 탄소 절감량을 계산하고, 정리 이력과 월별 통계를 제공합니다.

### FCM 알림

스캔 완료, 정리 완료, 스캔 권장 알림을 Firebase Cloud Messaging으로 전송해 사용자가 백그라운드 처리 결과를 확인할 수 있도록 합니다.

---

## 04. User Flow

```
Google 계정 로그인
   ↓
개인정보 수집 및 AI 분석 동의
   ↓
Gmail / Google Drive 권한 연결
   ↓
스캔 범위, 기간, 키워드, 파일 조건 설정
   ↓
Gmail / Drive 메타데이터 수집
   ↓
Gemini API 의미 분석
   ↓
Spring Boot Decision Engine 후보 확정
   ↓
정리 후보와 보호 대상 확인
   ↓
사용자가 삭제할 항목 선택 및 최종 승인
   ↓
Gmail / Drive 휴지통 이동
   ↓
정리 이력과 탄소 절감 통계 확인
```

---

## 05. Architecture

<img width="1535" height="1024" alt="제목 없음" src="https://github.com/user-attachments/assets/09e29373-ef02-484a-a70c-fe2002553729" />


---

## 06. ERD

<img width="4010" height="2482" alt="Copy of Copy of aura" src="https://github.com/user-attachments/assets/b717baf0-f158-4cc9-af09-0abf4a83cfbd" />



---

## 07. Key Highlights

### 메타데이터 중심 개인정보 보호

AURA는 Gmail 본문 전체와 Google Drive 파일 원문을 기본 분석 대상으로 사용하지 않습니다. Gemini API에는 분석에 필요한 제목, 일부 스니펫, 경로, 날짜, 크기, 라벨, 사용자 조건 중심의 제한된 정보만 전달합니다.

### Gemini API와 Decision Engine의 역할 분리

Gemini API는 의미 분석 신호를 생성하고, Spring Boot Decision Engine은 서비스 정책에 따라 최종 후보를 확정합니다. 이를 통해 AI의 유연한 의미 추론과 서버 코드의 안정적인 정책 검증을 함께 사용합니다.

### 사용자 승인 기반 안전 정리

AI 분석 결과는 삭제 명령이 아니라 정리 제안입니다. 실제 휴지통 이동은 사용자가 앱에서 항목을 확인하고 최종 승인한 뒤에만 수행됩니다.

### 중복 파일 및 보호 대상 탐지

Drive 파일의 `md5Checksum`, 파일명 유사도, 크기 정보, 공유 여부를 활용해 중복 가능성을 판단하고, 별표 메일, 중요 표시 메일, 공유 파일, 제외 키워드 매칭 항목은 보호 대상으로 분류합니다.

### 백그라운드 스캔과 알림

스캔 요청 후 사용자가 앱을 닫아도 서버에서 작업이 이어지며, 완료 시 FCM 알림으로 결과 확인을 유도합니다.

### Docker 기반 운영 배포

Spring Boot 서버는 Docker 이미지로 빌드되어 GHCR에 업로드되고, AWS EC2에서 Docker Compose와 Nginx Reverse Proxy를 통해 운영됩니다.

---

## 08. Services

### Auth Service

Google OAuth 로그인, AURA JWT 발급, Google Refresh Token 암호화 저장, 계정 연결 해제, 사용자 탈퇴 처리를 담당합니다.

### Scan Service

사용자의 스캔 요청을 생성하고, Gmail과 Google Drive의 메타데이터 수집 작업을 백그라운드에서 실행합니다.

### AI Analysis Service

수집한 메타데이터와 사용자 조건을 Gemini API 요청 형식으로 변환하고, 구조화된 AI 응답을 수신합니다.

### Decision Engine

Gemini 응답, 사용자 조건, 보호 규칙, 중복 탐지 결과를 조합해 최종 정리 후보와 보호 대상을 산출합니다.

### Cleanup Service

사용자가 최종 승인한 Gmail과 Drive 항목을 휴지통으로 이동하고, 작업 상태와 실패 항목을 기록합니다.

### Storage Service

저장소 화면에서 Gmail/Drive 항목과 휴지통 항목을 조회하고, 복구, 영구 삭제, 휴지통 비우기 흐름을 제공합니다.

### Statistics Service

정리 이력, 확보 용량, 예상 탄소 절감량, 월별 통계 데이터를 제공합니다.

### Notification Service

FCM 토큰을 관리하고 스캔 완료, 정리 완료, 스캔 권장 알림을 발송합니다.

### Infra Service

Docker Compose, Nginx, Certbot, GitHub Actions 배포 스크립트를 통해 EC2 운영 환경을 구성합니다.

---

## 09. Repositories

| Repository | Description |
| --- | --- |
| user-APP | React Native + Expo 기반 사용자 모바일 앱 |
| server | Spring Boot 기반 백엔드 API 서버 |
| AURA_infra | AWS EC2, Docker Compose, Nginx, HTTPS, CI/CD 배포 설정 |

---

## 10. Team

<table>
<tr>
<td align="center" width="20%">
<a href="https://github.com/junhyeok020630">
<img src="https://avatars.githubusercontent.com/junhyeok020630" width="72" height="72" alt="junhyeok020630" />
</a>
<br />
<b>junhyeok020630</b>
<br />
<sub>PM, AI, DevOps</sub>
</td>
<td align="center" width="20%">
<a href="https://github.com/gyn9208">
<img src="https://avatars.githubusercontent.com/gyn9208" width="72" height="72" alt="gyn9208" />
</a>
<br />
<b>gyn9208</b>
<br />
<sub>Backend</sub>
</td>
<td align="center" width="20%">
<a href="https://github.com/bongbongj">
<img src="https://avatars.githubusercontent.com/bongbongj" width="72" height="72" alt="bongbongj" />
</a>
<br />
<b>bongbongj</b>
<br />
<sub>Backend</sub>
</td>
<td align="center" width="20%">
<a href="https://github.com/ejunwon0701">
<img src="https://avatars.githubusercontent.com/ejunwon0701" width="72" height="72" alt="ejunwon0701" />
</a>
<br />
<b>ejunwon0701</b>
<br />
<sub>Frontend</sub>
</td>
</tr>
</table>
