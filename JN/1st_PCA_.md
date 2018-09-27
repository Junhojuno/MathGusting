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
  
##### 핵심 내용 : 데이터의 분산을 최대한 보존, 직교하는 새 기저축 찾아 Projection
  
> **More deeper Description**
<img src="https://latex.codecogs.com/gif.latex?&#x5C;small%20X&#x5C;in%20R^{_P&#x5C;times_N}%20:%20&#x5C;text{&#x5C;footnotesize%20원래데이터,%20%20input}"/>
<img src="https://latex.codecogs.com/gif.latex?A&#x5C;in%20R^{_N&#x5C;times_M}%20:%20&#x5C;text{&#x5C;footnotesize%20변환행렬,%20transformation%20function}"/>
<img src="https://latex.codecogs.com/gif.latex?Z&#x5C;in%20R^{_P&#x5C;times_M}%20:%20&#x5C;text{&#x5C;footnotesize%20변환%20후%20데이터,%20output}"/>  
  
 <p align="center"><img src="https://latex.codecogs.com/gif.latex?X%20*%20A%20=%20Z"/></p>  
  
 <p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;text{&#x5C;footnotesize%20결과적으로%20데이터%20갯수(Row)는%20그대로%20P개이고,%20feature%20갯수가%20N%20--&gt;%20M개로%20줄어들었다.(차원감소)}"/></p>  
 아래와 같이 **u,v라는 새 기저로 w를 Projection**하여 차원을 감소시켰다고 보는 것과 같다.
  
![선형변환](./img/linear_transformation.PNG ) <p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;text{&#x5C;tiny%20출처:%20ratsgo.github.io}"/></p>  
  
  
##### 어느 기저로 Projection해야 분산이 가장 크게 될까?
  
**이 문제는 <img src="https://latex.codecogs.com/gif.latex?Var["/>Xa<img src="https://latex.codecogs.com/gif.latex?]"/>를 최대로 하는 a(기저)를 찾는 문제가 된다.**
단, <img src="https://latex.codecogs.com/gif.latex?&#x5C;footnotesize%20X&#x5C;in%20R^{_N&#x5C;times_D},%20&#x5C;footnotesize%20a&#x5C;in%20R^{_D&#x5C;times_1}"/>이고 <img src="https://latex.codecogs.com/gif.latex?&#x5C;footnotesize%20E[X]=0"/>임을 가정하고 간다.
  
<img src="https://latex.codecogs.com/gif.latex?Var(Xa)%20=%20&#x5C;frac{1}{N}%20&#x5C;sum_{i}^{N}(Xa%20-%20E[Xa])^2"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;qquad%20&#x5C;qquad%20=%20&#x5C;frac{1}{N}%20&#x5C;sum_{i}^{N}(Xa%20-%20E[X]a)^2%20&#x5C;text{&#x5C;tiny%20(여기서%20E[Xa]%20=%20E[X]*a와%20같다)}"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;qquad%20&#x5C;qquad%20=%20&#x5C;frac{1}{N}%20&#x5C;sum_{i}^{N}(Xa)^2"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;qquad%20&#x5C;qquad%20=%20&#x5C;frac{1}{N}%20(Xa)^T(Xa)%20=%20&#x5C;frac{1}{N}%20a^TX^TXa"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;qquad%20&#x5C;qquad%20=%20a^T%20&#x5C;frac{X^TX}{N}a%20=%20&#x5C;underline%20&#x5C;bold%20{a^T%20&#x5C;sum%20a}"/>
  
<img src="https://latex.codecogs.com/gif.latex?&#x5C;bold{Loss}%20=%20a^T%20&#x5C;sum%20a%20-%20&#x5C;lambda(&#x5C;lVert%20a%20&#x5C;rVert^2-1)%20&#x5C;text{&#x5C;tiny%20&#x5C;quad%20a가%20커지면%20분산이%20그냥%20커진다는%20이유(?)로%20a를%20단위벡터로%20제한조건을%20걸었다..(이건%20좀%20더%20공부해야할%20부분)}"/>
<img src="https://latex.codecogs.com/gif.latex?{&#x5C;bold{&#x5C;large%20dL%20&#x5C;over%20da}}&#x5C;Longrightarrow%20(&#x5C;footnotesize%20&#x5C;sum%20+%20&#x5C;sum^T)a%20-%20&#x5C;lambda(I+I)a"/>
<img src="https://latex.codecogs.com/gif.latex?&#x5C;therefore%20&#x5C;bold{&#x5C;sum%20a%20=%20&#x5C;lambda%20a}%20&#x5C;Longrightarrow%20&#x5C;text{&#x5C;footnotesize%20이걸%20밑줄친%20부분에%20넣으면...}"/>
#### <img src="https://latex.codecogs.com/gif.latex?&#x5C;bold{argmax_a%20Var(Xa)%20=%20&#x5C;lambda}%20:%20&#x5C;text{&#x5C;footnotesize%20&#x5C;red{가장%20큰%20고유값이%20가장%20큰%20분산을%20의미}}"/>
  
  
즉 원 데이터의 **공분산행렬은 대칭행렬**이기 때문에 고유벡터들은 서로 직교한다.
이 공분산행렬을 고유분해하여 고유값/고유벡터를 구하고 각 고유값의 크기를 비교한다.
가장 큰 고유값이 가장 큰 분산을 의미한다.(분산을 가장많이 보존할 수 있다.)
PCA의 주성분 갯수를 정하고 그 갯수만큼 고유값을 큰 순서대로 고르고
**해당 고유값의 고유벡터들로 선형변환**을 실시하면 된다.
  
---
  
### 2. SVD(Singular Value Decomposition)
  
  
> 주요 키워드
 - Eigen Value Decomposition
 - Diagonal matrix
 - Singular value
  
 	 <p align="center"><img src="https://latex.codecogs.com/gif.latex?A=UΣV^T%20&#x5C;text{&#x5C;tiny%20(T%20:Transpose;전치행렬)}"/></p>  
  
  
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
  
  