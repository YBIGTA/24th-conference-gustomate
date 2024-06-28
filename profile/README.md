## Hi there 👋

# 자취생들을 위한 식재료 교환 플랫폼 생성

<div align="center">
<h3>24-1 YBIGTA 컨퍼런스</h3>

<em> 자취생들을 위한 식재료 교환 플랫폼 GustoMate입니다. Gusto는 스페인어로 "맛있는 음식을 먹는 즐거움"을 Mate는 "친구"를 의미합니다. 저희 팀명은 "음식의 즐거움을 나누는 친구"를 의미합니다. 
</em>

<div align="center">
    <img src="https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi" alt="FastAPI">
    <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
    <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/chatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white" alt="chatGPT">
    <img src="https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white" alt="AWS">
</div>
<div align="center">
    <img src="https://img.shields.io/badge/Python-3.12%2B-blue" alt="Python">
    <img src="https://img.shields.io/badge/OpenAI-API-green" alt="OpenAI">
</div>
<div>
    <img src="https://img.shields.io/badge/React_Native-orange" alt="React Native">
</div>


</div>

## 목차
- [문제 정의](#문제-정의)
- [데이터셋](#데이터셋)
- [모델링](#모델링)
- [백엔드](#백엔드)
- [프론트엔드](#프론트엔드)
- [결과 및 주요 기능](#결과-및-주요-기능)
- [팀 구성](#팀-구성)

## 문제 정의
*1인가구의 증가와 지속적인 물가 상승이 일어나고 있습니다. 하지만 한 번에 구입해야 하는 식재료의 양이 너무 많아 낭비가 발생합니다. 이를 해결하기 위해 식재료 교환 플랫폼을 만들고 필요한 식재료를 소량으로 교환하면 좋겠다고 생각했습니다.*


## 데이터셋
**데이터셋** *(사용한 데이터셋, API 등)*

- 음식 레시피
        - https://www.menupan.com/ 에서 1600개의 레시피를 크롤링 했습니다. 각 레시피 마다 난이도, 칼로리, 만드는데 필요한 주재료/부재료/양념, 만드는데 걸리는 시간, 만드는 방법 등 필요한 정보를 크롤링을 통해 얻어왔습니다. 
- OpenAi API
        - 추천 시스템 B에서 사용자의 기분과 최근에 먹은 메뉴를 반영해 최종메뉴와 그 이유를 추천합니다.
- mySQL
        - 백엔드 DB로 사용했습니다.
- Fast API
        - 백엔드
- Naver Clova OCR
        - 영수증 인식 OCR
- React Native
        - 프론트엔드
        
## 모델링

**모델링 기능 설명**:
   - 추천시스템 A: 사용자가 보유한 식재료들만 사용해서 만들수 있는 요리 추천
   - 추천시스템 B: 사용자의 선호도를 반영, 마켓에 있는 식재료들을 이용해 만들수 있는 요리 추천
     - 1단계: 각 음식을 벡터화(맵기, 테마, 칼로리, 난이도 등 이용)
     - 2단계: CF를 이용해 벡터화 한 음식들과 input으로 제공받은 사용자 정보 간의 코사인 유사도 계산
     - 3단계: 유사도가 가장 높은 10개의 메뉴 필터링
     - 4단계: OpenAi api를 이용, 사용자의 기분과 사용자가 최근에 먹은 메뉴를 반영해 3가지 메뉴를 이유와 함께 추천
     
   - [모델링 깃허브](https://github.com/GustoMate/Modeling)


  
## 백엔드

**백엔드 기능 설명**:
   - 회원가입, 사용자 선호도, 냉장고 식재료, 식재료 교환 마켓, 레시피 추천 기능 제공
   - [백엔드 깃허브](https://github.com/GustoMate/backend_fastAPI)


### 설치 방법

- `pip install "fastapi[all]"`
- `pip install python-dotenv`
- `pip install -r requirements.txt`

- 준비
  root 파일에 .env 생성 (openai key 유출 조심)

- 실행
  터미널에서 `uvicorn main:app --reload`실행
  http://127.0.0.1:8000/docs 에서 API 문서 확인 가능

파일구조:

```
GustomateApp
├── account
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── database
│   ├── database.py
│   └── models.py
├── dependency
│   └── dependencies.py
├── fridge
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── friend
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── ingredients
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── market
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── preference
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── recipe
│   ├── CRUD.py
│   ├── router.py
│   └── schema.py
├── README.md
├── config.py
├── create_Gustomate_Database.sql
├── main.py
└── requirements.txt


```



## 프론트엔드

**프론트엔드 기능 설명**:
   - 
   - [프론트엔드 깃허브](https://github.com/GustoMate/frontend)



## 결과 및 주요 기능

*(평가 지표, 구현한 핵심 기능 등)*

## 팀 구성

|이름|팀|역할|
|-|-|-|
|(팀장)이동진|DS|모델링|
|박수연|DS|백엔드|
|이우흥|DE|프론트/백엔드|
|류지현|DE|백엔드|
|김채연|DA|프론트|
|최정현|DA|모델링|
|오승옥|DA|모델링|

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
