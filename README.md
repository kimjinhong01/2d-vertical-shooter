# Unity 2D Top-down 슈팅 게임

![Game Preview](https://img.youtube.com/vi/RkmjT-Kpox4/0.jpg)

[**데모 영상 보기**](https://youtu.be/RkmjT-Kpox4)

---

## 프로젝트 개요

Unity 기반으로 제작된 세로형(top-down) 2D 슈팅 게임입니다.
플레이어는 다양한 적과 보스를 물리치며 스테이지를 클리어합니다.
직관적인 조작과 오브젝트 풀링 시스템을 통해 **퍼포먼스 최적화**를 구현한 것이 주요 특징입니다.

---

## 주요 기능

| 시스템         | 설명                                      |
| ----------- | --------------------------------------- |
| 적/보스 패턴 시스템 | 외부 텍스트 파일 기반 스폰 / 보스는 4가지 공격 패턴 순환 수행   |
| 플레이어 강화 시스템 | 아이템으로 파워업, 총알 수/종류 변화, 팔로워/폭탄 사용 가능     |
| 오브젝트 풀링     | `ObjectManager`에서 미리 생성해 Instantiate 제거 |
| 사운드 시스템     | `AudioManager` 싱글톤으로 BGM/SFX 재생 채널 관리   |
| 연출 및 UI     | 페이드, 폭발 이펙트, 무적 연출, 점수판, UI 안내 등        |

---

## 게임 플레이 흐름

```
Start → StageLoad → SpawnPattern → Combat → Boss → StageClear
         ↑                        ↓
       GameOver    ←    Player HP 0
```

1. `GameManager`가 스테이지 파일을 읽어 스폰 예약
2. 플레이어는 적을 처치하며 아이템을 수집해 강화
3. 일정 시간 후 보스 등장, 공격 패턴 수행
4. 보스를 처치하면 스테이지 클리어
5. 모든 스테이지 완료 시 게임 종료 / 체력 0이면 게임오버

---

## 코드 및 폴더 구조

```bash
Assets/
├── Scripts/
│   ├── GameManager.cs       # 스테이지 흐름 및 UI/스폰 관리
│   ├── ObjectManager.cs     # 풀링 시스템
│   ├── AudioManager.cs      # 사운드 관리
│   ├── Player.cs            # 이동/공격/파워업/피격
│   ├── Follower.cs          # 팔로워 공격/이동
│   ├── Enemy.cs             # 적/보스 공격 패턴
│   ├── Bullet.cs            # 총알 충돌/회전
│   ├── Explosion.cs         # 폭발 이펙트
│   ├── Background.cs        # 배경 스크롤
│   ├── Item.cs              # 아이템 드랍/효과
│   └── SpawnPattern.cs      # 스폰 데이터 구조
└── Resources/
    ├── Stage 0.txt
    ├── Stage 1.txt
    └── ...
```

---

## 조작 방법

| 기능   | 키보드 / 모바일 입력 | 설명                  |
| ---- | ------------ | ------------------- |
| 이동   | 방향키 / 조이스틱   | 8방향 자유 이동           |
| 공격   | Space / 버튼 A | 기본 총알 발사            |
| 폭탄   | Shift / 버튼 B | 전체 적 제거 + 탄막 삭제     |
| 무적모드 | X 키 (디버그)    | 무적 토글 ON/OFF (테스트용) |

※ 모바일은 9분할 터치 조이스틱 및 UI 버튼으로 동일 조작 가능

---

## 스테이지 패턴 파일 예시

```txt
# Stage 0.txt
1.0,A,3
2.5,B,5
4.0,C,7
10.0,boss,6
```

| 열  | 의미                             |
| -- | ------------------------------ |
| 1열 | 등장 딜레이 (초 단위)                  |
| 2열 | 적 타입 (`A`, `B`, `C`, `boss`)   |
| 3열 | 스폰 위치 인덱스 (`spawnPoints[0~9]`) |

---

## 실행 방법

1. Unity 프로젝트 열기 (권장 버전: Unity 2020.3 이상)
2. 메인 씬(`GameScene` 등) 실행
3. ▶ 버튼 클릭 → 게임 시작
4. 스테이지 자동 로딩 및 적 스폰

---

## 향후 개선 사항

* 스테이지 구성 편집 툴 (인게임/에디터)
* 보스 체력바 및 공격 예고 UI
* 난이도 모드 (Easy / Normal / Hard)
* 스테이지별 BGM 자동 전환
* 반응형 모바일 UI 강화
* AI 향상 (적 추적, 회피, 집단 움직임 등)

---

## 라이선스

```
본 프로젝트는 자유롭게 사용/수정/배포 가능하며, 상업적 사용 시 출처 표기를 권장합니다.
```

---

## 데모 영상 다시 보기

[![Demo Video](https://img.youtube.com/vi/RkmjT-Kpox4/0.jpg)](https://youtu.be/RkmjT-Kpox4)

[https://youtu.be/RkmjT-Kpox4](https://youtu.be/RkmjT-Kpox4)
