<div align="center">

### 교육 과정이 개인 계정에 매달리지 않도록, 그대로 복제해 둔 저장소.

AUTONOMOUS PCC의 자율주행 교육 과정이 서브모듈로 **고정(pin)** 해 쓰는<br>
[autorope/donkeycar](https://github.com/autorope/donkeycar) 미러입니다. 이 README 한 장을 제외하고 코드는 손대지 않았습니다.

![Mirror](https://img.shields.io/badge/저장소-Mirror-6B7280?style=for-the-badge)
![Upstream](https://img.shields.io/badge/Upstream-autorope%2Fdonkeycar-0B1B33?style=for-the-badge)
![Version](https://img.shields.io/badge/donkeycar-5.1.dev0-1E6FD9?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9-1E6FD9?style=for-the-badge)
![Pinned](https://img.shields.io/badge/고정커밋-d60dcb5e-16A34A?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**왜 있나**](#왜-이-저장소가-있나) · [**출처**](#출처) · [**어떻게 쓰이나**](#어떻게-쓰이나) · [**하지 말 것**](#하지-말-것) · [**원본 문서**](#원본-문서) · [**라이선스**](#라이선스)

<br>

```
autorope/donkeycar                 원본 (upstream)
        │  fork
        ▼
YUNSUNGWOONG/donkeycar             강사 개인 포크
        │  git push --mirror  ·  2026-10-10
        ▼
AUTONOMOUS-PCC-Inc/donkeycar       ← 이 저장소
        │  서브모듈로 SHA 고정
        ▼
aypi-car-tutorial                  바이브코딩 캠프 실습 저장소
```

<sub>전체 이력 <strong>2,185 커밋</strong>을 그대로 복제했습니다. 파일 216개, 변경 없음.</sub>

</div>

---

## 왜 이 저장소가 있나

교육용 실습 저장소가 **강사 개인 계정의 포크**를 서브모듈로 가리키고 있었습니다.
수업 당일 학생 수십 명이 동시에 클론하는 경로가 개인 계정 하나에 걸려 있는 상태입니다.

| 항목 | 내용 |
|---|---|
| **끊기면 수업이 멈춘다** | 개인 계정의 저장소 이름이 바뀌거나 비공개로 전환되면, 학생의 `git clone --recurse-submodules`가 그 자리에서 실패합니다. 설치 안내서 전체가 1단계에서 막힙니다. |
| **개인 포크의 브랜치는 움직인다** | 포크 소유자가 자기 브랜치에 무엇을 올리든 그것이 그대로 교육 자료의 의존성이 됩니다. 실제로 자매 저장소 [gym-donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar)에서 이 일이 일어났습니다. |
| **조직이 책임지는 사본이 필요하다** | 교육 과정은 회사 산출물입니다. 그 의존성도 조직 계정에 있어야 보존·접근 권한을 회사가 관리할 수 있습니다. |

> 그래서 코드를 바꾸지 않고 **이력 전체를 조직 계정으로 복제**했습니다.
> 업스트림을 대체하려는 것이 아니라, **교육 과정이 붙잡고 있을 고정점**을 만들기 위한 사본입니다.

---

## 출처

| 단계 | 저장소 | 비고 |
|---|---|---|
| 원본 | [`autorope/donkeycar`](https://github.com/autorope/donkeycar) | donkeycar 프로젝트 본체 (MIT) |
| 포크 | [`YUNSUNGWOONG/donkeycar`](https://github.com/YUNSUNGWOONG/donkeycar) | 강사 개인 포크 |
| 미러 | `AUTONOMOUS-PCC-Inc/donkeycar` | 이 저장소 · 2026-10-10 `git push --mirror` |

미러 푸시로 만들었기 때문에 GitHub에 **포크 배지가 표시되지 않습니다.** 이 문서가 그 출처 표기입니다.

**고정 커밋 `d60dcb5e0627465851873f35e80d3b3863973fc6`** (2023-12-20, `Update setup.cfg`)은
업스트림 `autorope/donkeycar`에 **같은 SHA로 존재하는 커밋**입니다.
즉 교육 과정이 쓰는 코드는 개인 포크에서 수정된 것이 아니라 업스트림 원본 트리입니다.

> 이 README 커밋의 **부모가 바로 그 고정 커밋**입니다.
> `main`의 끝점은 README가 올라가며 한 커밋 앞으로 움직였지만, 서브모듈이 가리키는 SHA는 그대로입니다.

---

## 어떻게 쓰이나

**AUTONOMOUS PCC 바이브코딩 캠프 1회차(자율주행)** 의 오전·오후 실습에서 `pip install -e .` 대상입니다.
Windows + conda 환경에서 donkeycar 라이브러리를 편집 가능 모드로 설치해, 학생이 `donkey` CLI와
`manage.py drive`로 시뮬레이터를 운전하고 행동 복제 모델을 학습시킵니다.

```bash
# 실습 저장소가 이 미러를 서브모듈로 끌어온다
git clone --recurse-submodules <aypi-car-tutorial>
cd <aypi-car-tutorial>/donkeycar
pip install -e .
donkey createcar --path ../cars/mycar
```

이 저장소를 단독으로 쓸 일은 없습니다. 설치 순서·conda 환경·시뮬레이터 설정은 실습 저장소의 안내서를 따르세요.

> 실습 저장소 `aypi-car-tutorial`은 준비 중이며, 현재 고정 주체는 [`YUNSUNGWOONG/DonkeyBro`](https://github.com/YUNSUNGWOONG/DonkeyBro)입니다.

---

## 하지 말 것

- **이 저장소에 이슈·PR을 올리지 마세요.** 코드 문제는 업스트림 [autorope/donkeycar](https://github.com/autorope/donkeycar/issues)로 가야 합니다. 여기는 사본입니다.
- **`git submodule update --remote`를 쓰지 마세요.** 고정된 SHA를 버리고 브랜치 끝점을 따라갑니다. 교육 과정에서는 항상 아래를 씁니다.

```bash
git submodule update --init --recursive   # 고정된 SHA를 체크아웃 (안전)
```

---

## 원본 문서

업스트림 README는 **고정 커밋 시점 그대로** 아래에 남아 있습니다.

- [README.md @ `d60dcb5e`](https://github.com/AUTONOMOUS-PCC-Inc/donkeycar/blob/d60dcb5e0627465851873f35e80d3b3863973fc6/README.md)
- 공식 문서 · [docs.donkeycar.com](https://docs.donkeycar.com)

---

## 라이선스

업스트림과 동일한 **MIT License**입니다. 원 저작권 표기를 그대로 보존했습니다.

```
MIT License

Copyright (c) 2017 Will Roscoe
```

전문은 [`LICENSE`](LICENSE)를 보세요. 이 미러는 저작권자를 바꾸지 않으며, 재배포 사본으로서 원 고지를 유지합니다.

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 교육 과정 의존성 미러</sub><br>
<sub>조직 소개 · <a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
