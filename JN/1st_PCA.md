## 1. PCA(Principle Component Analysis)

> 주요 키워드
 - 공분산 행렬
 - 고유값, 고유벡터
 - 선형변환
 - Projection
 - 대칭행렬과 직교(orthogonal)

Λ(고유값행렬-대각행렬)의 대각성분은 데이터 행렬 A의 각 변수에 해당하는 분산을 의미합니다.(라그랑쥬 승수법으로 증명) 
원 데이터의 분산을 최대화하는 새로운 기저를 찾는 것이 PCA 목표인 만큼 
가장 큰 고유값 몇 개를 고르고, 그에 해당하는 고유벡터를 새로운 기저로 하여 
원데이터를 Projection(선형변환)해주면 PCA 작업이 완료되게 됩니다.

즉 원 데이터의 공분산행렬은 대칭행렬이기 때문에 고유벡터들은 서로 직교한다.
이 공분산행렬을 고유분해하여 고유값/고유벡터를 구하고 각 고유값의 크기를 비교한다.
가장 큰 고유값이 가장 큰 분산을 의미한다.(분산을 가장많이 보존할 수 있다.)
PCA의 주성분 갯수를 정하고 그 갯수만큼 고유값을 큰 순서대로 고르고
해당 고유값의 고유벡터들로 선형변환을 실시하면 된다.

---

### 2. SVD(Singular Value Decomposition)

> 주요 키워드
 - Eigen Value Decomposition
 - Diagonal matrix
 - Singular value
  
 	 **A=UΣV^T** (T는 Transpose;전치행렬임을 의미)

기본적으로 행렬 A(NxM)는 아래 3개의 행렬의 곱으로 나타낼 수 있다.(Matrix Factorization; 행렬 인수분해)
 - U : NxN matrix(정방행렬, 모든 열벡터가 단위벡터;이를 특이벡터라 함, 각 열벡터는 서로 직교) 
 - Σ : NxM matrix(대각행렬, 대각성분이 행렬 A의 고유값의 제곱근;이것을 특이값이라 함, 내림차순 정렬, 0이상의 값)
 - V : MxM matrix(정방행렬, 모든 열벡터가 단위벡터;이를 특이벡터라 함, 각 열벡터는 서로 직교)

Σ의 비대각 성분들은 모두 0이다. 
그래서 비대각부분과 이것과 곱해지는 앞뒤행렬의 부분을 제거하고 곱해도 행렬 A를 구할 수 있다.
심지어 대각성분에서 0인 것들을 제거하여도 행렬 A를 구할 수 있다.

추가적으로 truncated SVD에서는 대각성분에서 상위 k개만 뽑아 A의 근사치를 구하는데
이것이 LSA(Latent Semantic Analysis, 잠재의미분석)에 활용된다.

---

### 3.LSA(Latent Semantic Analysis, 잠재의미분석)
 : 단어-문서행렬(Word-Document Matrix), 단어-문맥행렬(window based co-occurrence matrix) 등 입력 데이터에 특이값 분해를 수행해 데이터의 차원수를 줄여 계산 효율성을 키우는 한편 행간에 숨어있는(latent) 의미를 이끌어내기 위한 방법론.

> 특징
 - truncated SVD를 기반으로 작동한다.(상위 몇개의 고유값을 선택하여 추정한다.)

> 장점
 - 차원축소의 효과
 - 단어와 문맥 간의 내재적인 의미(latent/hidden meaning)을 효과적으로 보존할 수 있게 돼 결과적으로 문서 간 유사도 측정 등 모델의 성능 향상에 도움을 줄 수 있다.(Deerwester et ak.(1990)과 Landauer and Dumais(1997))
 - 입력 데이터의 노이즈 제거 (Rapp(2003))
 - 입력데이터의 sparsity를 줄일 수 있다.(Vozalis and Margaritis(2003))

> 단점
 - 새로운 문서나 단어가 추가되면 아예 처음부터 작업을 새로 시작해야함.
 
---

### 4.pLSA(Probabilistic Latent Semantic Analysis)
 : 단어와 문서 사이를 잇는, 우리 눈에 보이지 않는 잠재구조가 있다는 가정 하에 단어와 문서 출현 확률을 모델링한 확률모형

> 특징
 - LSA와 공유하는 개념이 많을 뿐 아예 다른 방법
 - Latent concepts(토픽의 가중치, 문서와 단어를 연결하는 역할)가 존재한다고 가정

> 필요개념
 - LSA
 - MLE(Maximum Likelihood Estimation)
 - EM(Expectation-Maximization) : pLSA의 학습 알고리즘
 
---

### 5.LDA(Latent Dirichlet Allocation)
