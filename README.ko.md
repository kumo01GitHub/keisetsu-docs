# keisetsu 문서

keisetsu의 전체 설계 의도와 운영 방침을 정리하는 문서 허브입니다.

`keisetsu-docs`는 각 구현 리포지토리(publisher / database / mobile)에 걸친 사양, 운영 규칙, 업데이트 절차를 통합 관리하는 장소입니다.

- 각 리포지토리의 책임을 명확히 함
- 배포 및 검증 플로우를 구현과 독립적으로 문서화
- 사양 변경 시 참고할 공통 판단 기준을 유지

## 컨셉

keisetsu는 학습 데이터의 보관 방법과 배포 경로를 공개하여 사용자가 직접 교재를 소유하고 사용할 수 있는 오픈소스 플래시카드 앱입니다.

- 목표
  - 누구나 스마트폰 하나로 학습할 수 있는 환경을 만드는 것
- 필요성
  - 데이터 비공개, 온라인 의존, 불투명한 업데이트 경로 등 기존 문제를 해결
- 우위성
  - 모든 사양, 데이터, 배포 플로우를 공개하여 투명성 보장
  - 오픈소스이므로 누구나 무료로 데이터를 갱신·이용 가능
- 실현 방침
  - 제작(publisher)·배포(database)·이용(mobile)을 분리하여 업데이트와 재사용이 쉬운 구조로 운영
  - 공개 스키마로 데이터 구조 통일, 공개 catalog로 배포 경로 명시, 오프라인 대응 앱으로 학습 가능하게 구성

## 사용자 가이드

### keisetsu 모바일 앱 사용법

1. 스마트폰에 Expo Go 앱을 설치하세요.
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. QR코드를 스캔하여 keisetsu 앱을 실행하세요.

![Expo QR](assets/eas-update.svg)

바로 keisetsu 앱을 사용할 수 있습니다.

### keisetsu 플래시카드 웹 에디터 사용법

1. [keisetsu-publisher 공개 페이지](https://keisetsu-publisher.vercel.app)에 접속
2. 새 덱을 만들거나 CSV/기존 kdb를 가져오기
3. 카드 및 덱 정보(ID, 제목, 언어 등) 편집
4. ZIP 파일 다운로드
5. 다운로드한 ZIP을 해제하고 생성된 파일을 keisetsu-database에 넣은 뒤 [추가/수정 요청](https://github.com/kumo01GitHub/keisetsu-database/issues) 제출

### 지원 언어

- 영어 (`en`)
- 일본어 (`ja`)
- 스페인어 (`es`)
- 포르투갈어 (`pt`)
- 중국어 (`zh`)
- 한국어 (`ko`)

## 개발자 가이드

자세한 리포지토리 구조, 운영 규칙, 기술 정보는 [DEVELOPER.md](./DEVELOPER.md)를 참고하세요.
