# 기여하기
## 데이터 구축 기여
* 형태소 분석기의 성능 개선은 모델 성능 향상뿐만 아니라 학습 데이터세트 품질도 중요하게 작용합니다.
* 모델의 성능을 높이는 가장 쉬운 방법은 데이터를 확장하는 것입니다. 
* 데이터 구축에 기여해주시면 더욱 똑똑한 형태소 분석기가 탄생할 수 있습니다.
* 데이터 구축에 기여하는 방법은 [한국어 모호성 평가 데이터세트](https://github.com/bareun-nlp/korean-ambiguity-data)의 말뭉치 오류를 수정 해주시거나 직접 형태소 분석된 문장들을 추가하는 방법이 있습니다.
* Contributor 혜택
  * 말뭉치 오류 수정 및 말뭉치 구축, 버그 제보, 기능 개선 제안 등 요청하시면 contributor 목록에 추가됩니다.


## Pull Request 방법
1. [한국어 모호성 평가 데이터세트](https://github.com/bareun-nlp/korean-ambiguity-data) 말뭉치 저장소를 본인의 계정으로 Fork합니다.
    * 이를 통해, 자신의 계정에 해당 프로젝트의 복제본이 생성됩니다.
2. 로컬 컴퓨터로 저장소를 복제하기(Clone)
    * Fork한 저장소를 로컬 컴퓨터로 복제합니다.
3. 수정할 말뭉치 작성 및 커밋(Commit)하고 푸시(Push)하기
    * 수정할 말뭉치 파일을 YAML로 작성하고, 로컬 저장소에서 이를 커밋합니다.
    * Github에 푸시(Push)합니다.
4. 원본 저장소에 풀 리퀘스트(Pull Request) 보내기
    * Fork한 저장소의 GitHub 페이지에서 "Pull Request" 버튼을 클릭합니다.
    * "Compare & pull request" 버튼을 눌러서 수정한 코드와 원본 저장소의 코드를 비교하고, 내용을 작성한 후 "Create pull request" 버튼을 누릅니다.

## YAML 형식
* bareun의 학습 데이터는 YAML 형식으로 구성됩니다.
* YAML을 사용하는 이유는 학습 데이터를 지속적으로 유지 보수 하는 데 있어서 편의성이 높고, 불필요한 따옴표나 기호 등이 사라져 가독성이 높기 때문입니다.
* 바른 학습데이터 말뭉치의 YAML 형식은 문장을 Key로 갖는 배열안에 token과 tag가 반복되는 구조입니다.
* 아래는 YAML 파일 형식의 예시입니다.
```
- 엄마가 마를 가셨다가 믹서기를 고장냈다.:
  - token: 엄마가
    tag: 엄마/NNG+가/JKS
  - token: 마를
    tag: 마/NNG+를/JKO
  - token: 가셨다가
    tag: 갈/VV+시/EP+었/EP+다가/EC
  - token: 믹서기를
    tag: 믹서기/NNG+를/JKO
  - token: 고장냈다.
    tag: 고장/NNG+내/VV+었/EP+다/EF+./SF
- 숙부께서 아빠에게 칼을 가셨다가 화를 누그러뜨렸다.:
  - token: 숙부께서
    tag: 숙부/NNG+께서/JKS
  - token: 아빠에게
    tag: 아빠/NNG+에게/JKB
  - token: 칼을
    tag: 칼/NNG+을/JKO
  - token: 가셨다가
    tag: 갈/VV+시/EP+었/EP+다가/EC
  - token: 화를
    tag: 화/NNG+를/JKO
  - token: 누그러뜨렸다.
    tag: 누그러뜨리/VV+었/EP+다/EF+./SF
- 할머니가 이를 가셨다가 다시 곤히 주무셨다.:
  - token: 할머니가
    tag: 할머니/NNG+가/JKS
  - token: 이를
    tag: 이/NNG+를/JKO
  - token: 가셨다가
    tag: 갈/VV+시/EP+었/EP+다가/EC
  - token: 다시
    tag: 다시/MAG
  - token: 곤히
    tag: 곤히/MAG
  - token: 주무셨다.
    tag: 주무시/VV+었/EP+다/EF+./SF
```
* '갈다'와 '가다' 경우, 일반적으로 말뭉치에 '가다' 동사의 빈도가 상대적으로 많으므로 '갈다'에 대한 데이터가 부족했습니다. 그래서 모델이 '가셨다가'를 '가/VV+시/EP+었/EP+다가/EC'로 분석할 가능성이 높습니다. 따라서 '갈/VV'의 의미로 사용된 문장을 추가로 학습시켜서 추론 성능을 높일 수 있습니다. 
