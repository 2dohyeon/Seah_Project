# Seah_Project
STS Round Bar Material Properties Prediction Service
# 스테인리스 봉강 물성 예측 서비스

### 1. 프로젝트 추진 배경

- 고객사는 기업에게 **특정 물성(물리적 성질)을 만족**하는 스펙의 봉강을 만들어달라고 요청함.
- 기업은 고객사에게 만든 제품을 납품하기 이전에 고객사의 요청 스펙에 만족하는지를 확인하기 위해 **필수적으로 품질보증과정이 진행**됨.
- 고객사에게 품질 보증서를 포함하여 최종 제품을 납품하게 됨.
- 필수적으로 진행되는 품질보증과정 속에서 현재 **두가지 문제점이 발생**하고, 이 문제를 해결하기 위함이 프로젝트의 목적임.

### 2. 프로젝트 목적

![Untitled](%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%87%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A1%E1%86%BC%20%E1%84%86%E1%85%AE%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%A8%E1%84%8E%E1%85%B3%E1%86%A8%20%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3%20e43ef01b2bc44071bda031a0e773c73a/Untitled.png)

- 품질보증과정에서 유효한 결과가 나올때까지 앞단의 과정이 반복진행되고 그에 따라 2가지 문제가 발생
    - **공정과정 지연문제** : 품질보증의 결과가 도출 될 때까지 후속과정을 진행할 수 없음
    - **공정상 부하문제** : 품질보증 시 유효한 물성수치가 도출되지 않을 시 추가 가공열처리 및 재시험 진행으로 앞단의 공정과정이 마비됨
- 품질보증과정 속 1회 시험을 진행되는 시간은 약 40분이며 연평균 약 1020회가 시행되므로 **연간 28일이나 소모**되는 과정임 (봉강 대상)
- 해당 시간소요 및 앞선 문제점을 **AI를 활용하여 완화ㆍ해결**하고자 함

### 3. 프로젝트 내용

   **3.1 프로젝트 방향**

- Two Step으로 진행하고자 하였고, **Step 01이 본 프로젝트의 주된 내용**임

![Untitled](%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%87%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A1%E1%86%BC%20%E1%84%86%E1%85%AE%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%A8%E1%84%8E%E1%85%B3%E1%86%A8%20%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3%20e43ef01b2bc44071bda031a0e773c73a/Untitled%201.png)

   3.2 Pain Point

- 데이터 수집 초기, 파편화된 데이터를 직접 수집하고 병합ㆍ전처리하는 과정에서 **데이터 결측치 및 소실 문제**로 회사 자체 기준에 대한 내용이 중요하게 작용하나 이를 파악하는데 어려움이 있었음
- 철강 분야의 경우 **제품의 크기, 구성성분의 함량에 따라 Target variable의 양상이 다르게** 보여 데이터셋을 적절한 기준을 두고 여러 Subgroup으로 나누어야 함.
- 철강 데이터의 경우 통계적인 방법에 기반한 EDA보다는 **철강 Domain 지식에 기반하여 Subgrouping 기준**을 세워야 함.

   3.3 Imporvements

- 초반 정의된 문제와 수집한 데이터셋의 분포로 보아 Multi-Output Regression 문제로 정의하였으나 Pain Point에 의해 **Subgrouping을 진행한 Target variable 별 Multi-Model**의 형태로 접근함.
- 주어진 **데이터의 Target variable의 특성을 기준**으로 하여 큰 영향을 미치는 주요 feature를 선별하여 **K-means에 기반한 Subgrouping**을 진행함
- **PCP (Parallel Coordinates Plot) 을 활용한 재료공학적 접근을 시도**하여 구성원소별 특징, Target variable에 영향을 주는 요인을 파악하고 feature selection을 진행함.
- 모델링과정에서 **AutoML**을 사용하여 정해진 시간내 다양한 결과를 파악하고자 하였음.
- 최종적으로 **XGBoost**를 사용하여 Subgrouping 모델링을 한 결과 **전/후 평균 17%p 정도의 R-Square 향상을 이뤄냄**
    
    ![Untitled](%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%87%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A1%E1%86%BC%20%E1%84%86%E1%85%AE%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%A8%E1%84%8E%E1%85%B3%E1%86%A8%20%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3%20e43ef01b2bc44071bda031a0e773c73a/Untitled%202.png)
    
    ![Untitled](%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%87%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A1%E1%86%BC%20%E1%84%86%E1%85%AE%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%A8%E1%84%8E%E1%85%B3%E1%86%A8%20%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3%20e43ef01b2bc44071bda031a0e773c73a/Untitled%203.png)
    

   3.4 Prototype

- 품질보증 관계자의 편의성을 고려하여 웹 대시보드 형태로 프로토타입을 제작하였으며 부가적인 기능을 추가하고자 함.

- 물성 예측 모델을 연결하여 구축한 웹을 통해 사용자가 입력한 indepent variable에 따라 예측된 target variable를 시각적으로 확인 가능

![Untitled](%E1%84%89%E1%85%B3%E1%84%90%E1%85%A6%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%20%E1%84%87%E1%85%A9%E1%86%BC%E1%84%80%E1%85%A1%E1%86%BC%20%E1%84%86%E1%85%AE%E1%86%AF%E1%84%89%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%A8%E1%84%8E%E1%85%B3%E1%86%A8%20%E1%84%89%E1%85%A5%E1%84%87%E1%85%B5%E1%84%89%E1%85%B3%20e43ef01b2bc44071bda031a0e773c73a/Untitled%204.png)

※ 기업데이터 보안문제상 프로토타입에 보여지는 데이터는 임시데이터로 교체되어있습니다

### 4. Future Work

- **Model 성능개선** : 현재 철강 Domain에 기반한 SubGrouping이 진행되었다. 이 과정 속 해결하지 못했던 문제점은 같은 독립변수 조합을 가지나 다른 target variable 값을 가지는 것을 확인하였다. 공정과정 속 데이터 수집ㆍ확보 면에서 이 데이터를 구분지을 수 있는 또 다른 독립변수인 열처리 데이터가 충분히 확보되어 모델링을 진행한다면 확실한 성능개선이 이어질 것이라고 생각이 들었다.
- **Service UX 개선** : 품질보증을 진행하는 연구원들 입장에서의 서비스를 고려하여 제작하였다. 기업측에서 피드백한 바로는 물성예측하는 부분은 유효하나, 나머지 부분은 잘 모르겠다고 하여 해당부분에 집중한 UI/UX 및 서비스 개선을 진행해볼 수 있을 것이다.
- **After Work** : 본 프로젝트 이후 Step 01에 대한 성능을 끌어올린다면 Step 02에 대한 내용까지 진행될 수 있을 것이며 그렇게 된다면 기업입장에서는 더 큰 기대효과를 얻을 수 있을것이라 생각한다.
