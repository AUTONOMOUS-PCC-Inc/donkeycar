<div align="center">

<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/donkeycar-banner.svg" alt="donkeycar — 수업에서 쓰는 라이브러리. 160x120 카메라 이미지에서 조향값과 속도를 내는 행동 복제" width="100%">

### 네 차를 움직이는 라이브러리. 이 폴더가 그거다.

[실습 저장소](https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial)를 클론할 때 **같이 따라온 폴더**입니다. 따로 내려받을 필요 없습니다.<br>
여기서 할 일은 설치 한 번뿐이고, 나머지는 안내서를 따라가면 됩니다.

![Version](https://img.shields.io/badge/donkeycar-5.1.dev0-1E6FD9?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9-1E6FD9?style=for-the-badge)
![Env](https://img.shields.io/badge/conda-aypi--car-16A34A?style=for-the-badge)
![OS](https://img.shields.io/badge/수업환경-Windows-0B1B33?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**여기서 할 일**](#여기서-할-일은-설치-한-번) · [**수업에서 어디에 쓰나**](#수업에서-어디에-쓰나) · [**용어**](#처음-보는-말들) · [**안 될 때**](#잘-안-될-때) · [**출처**](#이-저장소에-대해)

</div>

---

## 여기서 할 일은 설치 한 번

conda 환경 `aypi-car`를 켠 상태에서, **이 폴더 안에서** 다음을 실행합니다.

```bash
conda activate aypi-car
cd donkeycar
pip install -e .
```

`-e`는 "editable", 즉 **복사해 가지 않고 이 폴더를 그대로 가리키는** 설치입니다.
그래서 설치가 끝난 뒤에 이 폴더를 다른 데로 옮기면 깨집니다. 옮기지 마세요.

설치가 됐는지는 이걸로 확인합니다.

```bash
donkey --help
```

명령 목록이 나오면 끝입니다. 그다음은 안내서로 돌아가세요.

> 설치 순서 전체·conda 환경 만들기·시뮬레이터 내려받기는 **설치 안내서**에 있고,
> 실습 저장소는 [`AUTONOMOUS-PCC-Inc/aypi-car-tutorial`](https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial)입니다.
> 이 문서는 "이 폴더가 뭐였더라" 싶을 때 보는 보조 문서입니다.

---

## 수업에서 어디에 쓰나

하루 일정의 여섯 단계를 전부 이 라이브러리가 떠받칩니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/donkeycar-pipeline.svg" alt="6단계 수업 흐름: 설치 · 차량 생성 · 데이터 수집 · 학습 · 자율주행 · 바이브코딩 과제" width="100%">
</div>

핵심만 말하면 이렇습니다. **네가 시뮬레이터에서 운전한 기록을 모아서, 그걸
흉내 내는 모델을 학습시키고, 그 모델에게 운전을 맡긴다.** 이걸 행동 복제라고 부릅니다.

모델이 잘 못 달리면 그건 대개 모델이 멍청해서가 아니라 **네 운전 기록에 그 상황이
없어서**입니다. 오후 과제가 바로 그 지점을 찾는 일입니다.

3·5단계는 시뮬레이터에 붙는 계층이 하나 더 필요합니다 —
[`gym-donkeycar`](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar) 폴더가 그 역할입니다.

---

## 처음 보는 말들

| 말 | 뜻 |
|---|---|
| **tub** | 주행 기록 한 통. `data/` 폴더가 tub입니다. 안에 카메라 사진(`images/`)과, 사진마다 네가 준 조향값·속도가 들어 있습니다. |
| **pilot / model** | 학습 결과물. `models/mypilot.h5` 한 파일입니다. 사진을 넣으면 조향값과 속도를 뱉습니다. |
| **part** | 주행 루프에 끼워 넣는 부품 하나. 카메라도 part, 조이스틱도 part, 모델도 part입니다. |
| **myconfig.py** | 네 차 설정 파일. 시뮬레이터를 쓸지, 어떤 트랙을 쓸지 여기서 정합니다. |
| **epoch** | 학습이 데이터 전체를 한 번 훑는 것. 수십 번 반복하면서 조금씩 나아집니다. |

---

## 잘 안 될 때

| 증상 | 원인과 해결 |
|---|---|
| `donkey` 명령을 찾을 수 없다 | 십중팔구 **conda 환경을 안 켰습니다**. `conda activate aypi-car` 먼저. 환경을 켰는데도 안 되면, 설치한 뒤에 이 폴더를 옮기지 않았는지 보세요 (editable 설치라 경로가 바뀌면 깨집니다). 옮겼다면 `pip install -e .`를 다시 돌리면 됩니다. |
| `Could not load dynamic library 'cudart64_110.dll'` 가 아홉 줄쯤 뜬다 | **정상입니다.** GPU가 없어서 TensorFlow가 CPU로 돌겠다고 알리는 것뿐입니다. 학습도 주행도 그대로 됩니다. 인터넷에 "opencv를 지우면 된다"는 글이 있는데 **따르지 마세요** — 원인이 다릅니다. |
| 학습이 끝날 기미가 없다 | 원래 오래 걸립니다. 노트북 CPU에서 몇천 장이면 수십 분입니다. 시작해 놓고 **건드리지 말고** 기다리세요. 중간에 창을 닫으면 처음부터입니다. |
| 폴더가 텅 비어 있다 | 서브모듈을 안 받은 것입니다. [실습 저장소](https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial) 맨 위에서 `git submodule update --init --recursive`. |
| 시뮬레이터에 연결이 안 된다 | 이 폴더 문제가 아닙니다. [`gym-donkeycar`](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar) 쪽 안내를 보세요. |

그래도 안 되면 **에러 메시지 전체를 복사해서** 강사에게 보여 주세요.
마지막 줄만 보면 원인을 못 찾는 경우가 많습니다.

---

## 하지 말 것

- **`git submodule update --remote` 금지.** 수업이 고정해 둔 버전을 버리고 최신으로 끌어옵니다. 항상 `git submodule update --init --recursive` 를 쓰세요.
- **이 저장소에 이슈·PR 금지.** 여기는 수업용 사본입니다. 라이브러리 자체의 문제는 원본 [autorope/donkeycar](https://github.com/autorope/donkeycar/issues)로 가야 합니다.
- **설치 후 폴더 이동 금지.** 위에 적은 이유로 깨집니다.

---

## 이 저장소에 대해

[autorope/donkeycar](https://github.com/autorope/donkeycar)를 **그대로 복제한 사본**입니다.
수업이 개인 계정에 의존하지 않도록 회사 조직 계정에 두었습니다. 이 README 한 장
말고는 코드를 손대지 않았고, 수업이 쓰는 커밋은 원본에 **같은 SHA로 존재하는**
커밋이라 네가 설치하는 건 원본 코드 그대로입니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/donkeycar-provenance.svg" alt="출처 사슬: autorope 원본 → 개인 포크 → AUTONOMOUS PCC 미러 → 실습 저장소" width="100%">
</div>

| 단계 | 저장소 |
|---|---|
| 원본 | [`autorope/donkeycar`](https://github.com/autorope/donkeycar) |
| 포크 | [`YUNSUNGWOONG/donkeycar`](https://github.com/YUNSUNGWOONG/donkeycar) |
| 사본 | `AUTONOMOUS-PCC-Inc/donkeycar` · 2026-10-10 `git push --mirror` |

고정 커밋은 `d60dcb5e0627465851873f35e80d3b3863973fc6` (2023-12-20)입니다.
미러 푸시라 GitHub에 포크 배지가 안 붙으므로, 이 절이 출처 표기입니다.

**원본 README**는 그 커밋 시점 그대로
[여기](https://github.com/AUTONOMOUS-PCC-Inc/donkeycar/blob/d60dcb5e0627465851873f35e80d3b3863973fc6/README.md)에
남아 있고, 공식 문서는 [docs.donkeycar.com](https://docs.donkeycar.com)입니다.

### 라이선스

원본과 같은 **MIT License**이고 원 저작권 표기를 그대로 보존했습니다.

```
MIT License

Copyright (c) 2017 Will Roscoe
```

전문은 [`LICENSE`](LICENSE)에 있습니다.

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 바이브코딩 캠프 1회차 실습용</sub><br>
<sub><a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
