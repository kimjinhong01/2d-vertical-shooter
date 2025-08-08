# Unity 2D Shooting Game

![Game Preview](https://img.youtube.com/vi/RkmjT-Kpox4/0.jpg)
> [데모 영상 보기](https://youtu.be/RkmjT-Kpox4)

---

## 프로젝트 개요

Unity 기반으로 제작된 세로형(Top-down) 2D 슈팅 게임입니다.  
플레이어는 다양한 적과 보스를 물리치며 스테이지를 클리어해야 하며, 조작의 직관성과 오브젝트 풀링을 활용한 퍼포먼스 최적화가 특징입니다.

---

## 주요 기능

- 다양한 적과 보스 패턴  
  외부 텍스트(`Stage 0.txt`, `Stage 1.txt` 등) 기반으로 구성된 스폰 패턴 사용  
  보스는 4가지 공격 패턴을 순차 수행: 정면 사격, 산탄, 곡선, 전방위

- 플레이어 강화 시스템  
  파워 단계에 따라 총알 수와 종류 변화  
  팔로워(Follower) 유닛 추가 및 강화  
  폭탄 사용으로 전체 적 제거 가능

- 오브젝트 풀링 시스템  
  `ObjectManager`에서 적, 총알, 아이템 등을 미리 생성해 퍼포먼스 최적화

- 사운드 시스템  
  `AudioManager` 싱글톤으로 배경음(BGM)과 효과음(SFX)을 채널 방식으로 재생

- 풍부한 연출과 UI  
  페이드 전환, 폭발 이펙트, 스테이지 시작/클리어, 점수판, 무적모드, 리스폰 연출 등

---

## 디렉토리 및 코드 구조

```
Assets/
 ├── Scripts/
 │    ├── GameManager.cs         # 스테이지 흐름, UI, 스폰 관리
 │    ├── ObjectManager.cs       # 오브젝트 풀링 처리
 │    ├── AudioManager.cs        # 효과음/배경음 재생
 │    ├── Player.cs              # 이동, 공격, 파워업, 피격 처리
 │    ├── Enemy.cs               # 일반/보스 적의 공격 패턴
 │    ├── Follower.cs            # 팔로워 유닛 동작/공격
 │    ├── Bullet.cs              # 총알 회전/충돌 처리
 │    ├── Explosion.cs           # 폭발 이펙트 처리
 │    ├── Background.cs          # 스크롤 배경
 │    ├── Item.cs                # 아이템 낙하/효과
 │    └── SpawnPattern.cs        # 스폰 패턴 데이터 구조
 └── Resources/
      ├── Stage 0.txt, Stage 1.txt, ...
```

---

## 조작 방법

| 기능       | 키보드 / 모바일 입력 | 설명                         |
|------------|-----------------------|------------------------------|
| 이동       | 방향키 / 조이스틱     | 8방향 자유 이동             |
| 공격       | Space / 버튼 A        | 총알 발사                   |
| 폭탄       | Shift / 버튼 B        | 적 전체 제거 + 탄막 삭제    |
| 무적 모드  | X 키                  | 디버그용 토글 (ON/OFF)      |

모바일 환경에서는 9분할 터치 조이스틱과 UI 버튼을 통해 조작 가능합니다.

---

## Stage 패턴 파일 예시 (`Stage 0.txt`)

```txt
1.0,A,3
2.5,B,5
4.0,C,7
10.0,boss,6
```

- 1열: 등장 딜레이 (초)
- 2열: 적 타입 (`A`, `B`, `C`, `boss`)
- 3열: 스폰 위치 인덱스 (1~10, `spawnPoints` 배열 기반)

---

## 주요 시스템 설명

### GameManager.cs
- 스테이지 로딩 및 진행 흐름 관리
- 적/보스 스폰, UI 출력, 게임 클리어/오버 처리

### ObjectManager.cs
- 모든 게임 오브젝트를 풀링으로 미리 생성
- `MakeObj()`, `GetPool()`로 불필요한 Instantiate 방지

### Player.cs
- 이동/공격/파워 업/폭탄/피격/아이템 처리 모두 담당
- 팔로워 유닛 강화 및 무적 모드 등 기능 포함

### Enemy.cs
- 일반 적은 자동 사격
- 보스는 패턴 기반 공격 (4종류)
- 체력 시스템 및 아이템 드롭 포함

### Follower.cs
- 플레이어의 움직임을 Queue로 추적
- Power 단계에 따라 최대 4기까지 활성화
- 자동 사격 지원

---

## 게임 플레이 흐름

1. `GameManager`가 스테이지 텍스트 파일을 읽고 스폰 패턴 준비
2. `Player`는 기본 공격으로 적을 처리하며 아이템을 수집해 강화
3. 적은 패턴 또는 랜덤으로 등장하며 공격 수행
4. 보스를 처치하면 `StageClear()` → 다음 스테이지
5. 모든 스테이지 클리어 시 게임 종료
6. 체력 0이면 `GameOver()` 처리 및 점수판 출력

---

## 향후 개선 사항

- 스테이지 패턴을 Unity 에디터 상에서 구성할 수 있는 편집기
- 보스 체력바 및 공격 사전 예고 UI
- 난이도 조정 기능 (Easy / Normal / Hard)
- 스테이지별 BGM 자동 전환
- 조작 및 UI의 모바일 반응형 최적화
- 플레이어 및 적 AI 강화 (추적, 회피, 집단 이동 등)

---

## 라이선스

```
MIT License

Copyright (c) 2025 ...

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 데모 영상

[![Demo Video](https://img.youtube.com/vi/RkmjT-Kpox4/0.jpg)](https://youtu.be/RkmjT-Kpox4)  
https://youtu.be/RkmjT-Kpox4
