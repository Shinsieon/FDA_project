# FDA_project
## <금융데이터 분석 수업에서 진행한 기말 프로젝트>
> 최근 코로나19로 인한 전 세계적 팬데믹 현상과 더불어 4차 산업혁명 관련 기술의 발달로 인하여 노동시장에서의 불안정성이 커지고 저금리 기조가 지속되는 가운데 개인과 가계 단위의 투자자들이 재무 설계와 위험관리에 대한 관심이 점차 급증하고 있다. 투자자들은 점차 증가하는 불확실성 하에서 투자를 결정할 때 자신에게 가장 적합한 대안을 선택할 수 있어야 하며 투자자의 위험을 대하는 태도에 따른 투자 성향을 구분하여 투자 의사결정을 해야 한다. 특히, 주식시장에서 주식가격은 다양하고 불확실한 여러 요인에 의해 영향을 받기 때문에 주가변동의 이유를 정확하게 파악하는 것은 매우 어렵다. 하지만 주가를 결정하는 기업의 미래수익 및 할인율은 거시경제변수에 의해 영향을 받으므로 거시적인 관점에서 거시경제변수의 변동이 주가변동의 주요 요인이 될 수 있다. 이자율 기간구조에는 미래 경제상황에 대한 경제주체의 다양한 기대가 반영되어 있다. 특히 유동성이 높은 채권시장 거래에서 결정되는 장단기 이자율 격차인 이자율 스프레드는 시장참가자의 미래 지향적 기대가 잘 반영되어 있다. 따라서 본 연구는 실물경제 데이터인 GDP(Gross Domestic Product) 와 채권 Yeild Spread(U.S.10Year Treasury-Federal Funds Rate)를 통하여 미래 경제를 예측한 후 주식가격을 예측하여 개인의 투자성향에 따른 맞춤형 포트폴리오 제안을 목적으로 한다. 포트폴리오 최적화 시 개인 투자자의 투자 성향 뿐만 아니라 과거의 경제 상황의 산업군 별 수익률 순위와 거래 비용을 최소화하기 위한 Turn Over 제약을 추가하여 개인 투자자의 보다 효과적인 재무 설계와 위험관리를 하고자 하였다. 본 연구에서는 1960년부터 1999년까지의 실물경제 데이터와 금융데이터를 기계학습을 이용하여 훈련시켰으며 이후 2000년부터 2020년 10월까지를 Test 기간으로 설정하였다.

## Table of Contents
_Note: This is only a navigation guide for the specification, and does not define or mandate terms for any specification-compliant documents._

- [Sections](#sections)
  - [Data](#data)
  - [Modeling](#modeling)
  - [Methodology](#methodology)
  - [UI](#ui)
  - [Maintainers](#maintainers)
  - [Installation](#installation)

## Sections

### Data
- 독립변수 
  * GDP 구성 요소 중 Personal Consumption : Durable Goods, Non-Durable Goods, Services
  * Investment : Business investment, Fixed Investment 
  * 정부 지출 : Government Total Spending
  * GDP 성장률
  * 미국채 10년물 금리
- 종속변수
  * positive 는 추후 3개월의 수익률이 1960년부터 2000년까지 S&P500 지수의 3개월 평균 수익률인 약 2.4%보다 높을 때, negative는 수익률이 음수일 때, moderate는 2.4%와 0 사이인 경우로 나누어 카테로기컬한 변수를 만들었다.
- 포트폴리오에 사용되는 자산 SET : Fama-french 5 industry, Fama-french 10 industry
- 투자성향 분석 : 투자성향에 관한 5가지 설문에 대해 4점 척도를 활용하여 투자자에게 맞는 투자성향을 산출하고자 하였다. `김지영, 2011`

### Modeling
- 각 모델 별로 Cross Validation 한 후 차이를 나타내는 표이다. Decision tree regressor의 평균과 분산이 다른 모델보다 우수한 성능을 보여주어 본 연구에서는 Decision Tree regressor 기법을 사용하여 모델링을 진행하였다. 해당 모델의 성능은 1960년부터 1999년 동안  트레이닝을 할 때의 정확도는 75% 였으나 2000년 이후의 데이터를 활용하여 예측을 했을 때의 정확도는 약 65% 다. 아래 그림에서 각 변수의 중요도를 확인할 수 있는데 본 연구에 사용된 모델에서 예측할 때 가장 중요한 변수는 yield spread 임을 알 수 있다.

![image](https://user-images.githubusercontent.com/56333934/102740610-9987cf00-4393-11eb-90f2-2f21052889ef.png)

- 아래 그림은 본 연구에 사용되는 모델로 3개월 후의 S&P500의 수익률을 Negative로 예측한 경우 S&P500을 Short 하고 3개월 후의 S&P500의 수익률을 Positive로 예측한 경우 S&P500을 Long 한 경우와 경제상황과 무관하게 S&P500을 보유했을 때의 차이를 나타낸 그래프이다

![image](https://user-images.githubusercontent.com/56333934/102776640-703a6380-43d2-11eb-8b19-9368c8b90e2b.png)

### Methodology
- 평균 분산 모형 (Mean-Variance Model)
Mean-Variance 분석은 현대 포트폴리오 이론 중에 하나이며, 모든 투자자들은 완전정보를 가지고 가장 이성적인 투자결정을 한다는 가정과 위험은 적고 기대수익률은 높은 전략을 세운다는 것을 가정한다. 평균-분산 모형에는 분산과 기대수익률로 구성되어있다. 현대 포트폴리오 이론에서 투자자는 각자의 성향에 따라 분산 수준과 기대수익률 수준을 정해 포트폴리오를 구성할 수 있으며 이러한 전략의 목적은 빠르게 변하는 시장 상황에 따른 큰 손실을 방지할 수 있게 하는 것이다. 본 연구는 프로그램의 가장 기본이 되는 모형을 평균-분산 모형으로 설정하였으며 모든 투자자의 목적은 분산의 최소화라는 가정 하에 목적함수를 세웠다
  * 제약식
  ![image](https://user-images.githubusercontent.com/56333934/102776864-d6bf8180-43d2-11eb-9e76-6a27d3bc4bb3.png)
    1. No shorting 공매도는 주가 하락이 예상되는 종목의 주식을 미리 빌려서 팔고 나중에 실제로 주가가 내려가면 싼값에 다시 사들여 빌린 주식을 갚아 차익을 남기는 투자 기법이다. 개인 투자자의 경우 공매도의 실현이 어렵기 때문에 공매도 금지 제약을 추가하였다.

    2. Turn Over 포트폴리오의 Turn Over는 펀드 매니저 혹은 투자자가 자산을 매수와 매도하는 빈도를 측정하는 값이다. 포트폴리오의 비중 변화가 일정 값()이 되게 설정해주는 것이다. 하지만, 본 연구의 경우 다른 제약과의 충돌로 초기값 0.1 로 제한을 두었을 때 최적해를 찾지 못하는 상황이 빈번히 발생하였다. 이를 해결하기 위해서 초기값 0.1에서 최적해를 찾을 때까지 0.1씩 추가하여 최적화를 반복 시행하는 알고리즘을 작성하였다.

    3. Rank 1절에서 설명한 머신러닝 모델에 의해 나온 결과 값은 투자 시점을 기준으로 추후 3개월의 시장 상황 예측 값으로 positive, negative, moderate 세 가지로 분류된다. positive 는 추후 3개월의 수익률이 1960년부터 2000년까지 S&P500 지수의 3개월 평균 수익률인 약 2.4%보다 높을 때, negative는 수익률이 음수일 때, moderate는 2.4%와 0 사이인 경우를 의미한다. 이를 제약식에 추가하기 위해서 다음과 같은 분석 과정을 거쳤다.
    
      - 1960년부터 2000년까지의 월별 수익률 데이터를 구한다. 자산은 Fama-French 5,10 industry 로 구성하였다.
      - S&P500 월별 수익률 데이터와 결합(Concat) 후 3개월 기하 평균 수익률로 변환한다.
      - S&P500 3개월 평균 수익률인 2.4%를 기준으로 Positive, Negative, Moderate 세 경우의 데이터프레임으로 나눈다.
      - 나눠진 데이터프레임에서 평균 수익률 순위를 구한 후 제약식에 추가한다. wH: 수익률이 가장 높았던 자산, WL: 수익률이 가장 낮았던 자산을 의미한다.
      - 만약 추후 3개월의 경제 상황이 positive라면 과거 positive였던 시기 중 수익률이 가장 높았던 자산()은 수익률 하위 50% 자산들보다 더 많은 비중으로 투자를 한다. 또한, 과거 positive였던  시기 중 수익률이 가장 낮았던 자산()은 수익률 상위 50% 자산들보다 적은 비중으로 투자를 한다. 알고리즘을 위와 같이 구성한 이유는 단순히 수익률을 내림차순으로 비중을 설정했을 때 (수익률 최고 자산>2위 자산>3위 자산>….>수익률 최저 자산) 제약식에 많은 충돌이 일어났고 최적해를 찾지 못했기 때문이다.

    4. 채권 비중 본 연구의 프로그램은 최적 포트폴리오를 계산할 때 개인 투자자의 투자성향까지 고려해준다. 투자성향은 개인투자자의 투자성향에 따른 금융자산 포트폴리오를 참고하여 투자자의 설문조사 답변에 따라 “안정형, 위험 중립형, 공격 투자형“ 세 가지 유형으로 분류하였다.(김지영, 2011) 각 투자유형을 다음과 같이 정의하였다.
    
      - 안정형은 예, 적금 수준의 수익률을 기대하며, 투자원금에 손실이 발생하는 것을 원하지 않는다.
      - 위험 중립형은 투자에는 그에 상응하는 투자위험이 있음을 충분히 인식하고 있으며, 예, 적금보다 높은 수익을 기대할 수 있다면 일정 수준의 손실위험을 감수할 수 있다.
      - 공격 투자형은 시장평균 수익률을 훨씬 넘어서는 높은 수준의 투자수익을 추구하며, 이를 위해 자산가치의 변동에 따른 손실 위험을 적극 수용하고 투자자금 대부분을 주식, 주식형펀드 또는 파생상품 등의 위험자산에 투자할 의향이 있다. 따라서 본 연구는 사용자의 투자성향이 안정형일 경우 채권의 비중을 0.6, 위험 중립형의 경우 0.4, 공격 투자형은 0.2로 제한을 두었다. 분산을 최소화하는 것이 목적함수이기 때문에 주식에 비해 분산이 낮은 채권의 비중에 대한 제약식을 추가하였다.

- 백테스트
  * 투자자 입력사항
    - 투자자는 본 연구의 프로그램에 투자 시작일, 투자 종료일, 투자 금액, 투자하고자 하는 자산군, 투자성향에 관한 설문 문항, Lookback Period를 입력한다. 여기서 투자 자산은 ‘Fama-French 5 Industry‘, ‘Fama-French 10 Industry‘ 중 1개를 선택하여 입력하며, 두 데이터프레임 모두 기존 ‘Others’ 자산을 미 국고채 10년물 채권으로 대체하였다. 투자성향에 관한 5가지 설문에 대해 4점 척도를 활용하여 투자자에게 맞는 투자성향을 산출하고자 하였다. (김지영, 2011). 5가지 설문에서 사용자가 입력한 값을 토대로 점수의 총 합이 각각 “10이하, 10초과 15미만, 15이상” 일 때 안정형, 중립형, 공격형을 나누었다.
  * 투자성향에 따른 최적화된 Rebalancing 비중 산출
    - 투자자의 투자성향에 따라 각 포트폴리오 비중 최적화 간에 초기 비중을 아래 표와 같이 지정하였다. 주식 내 자산군들의 초기 비중은 정해진 주식의 비중 하에서 균등하게 투자한다고 가정하였다. 예를 들어 ‘Fama-French 5 Industry’에 투자하는 안정형의 투자자라면 주식 4개와 채권 1개에 대하여 각각 [0.1, 0.1, 0.1, 0.1]과 0.6의 비중으로 투자를 시작한다. 이후 Rebalancing에 있어서 초기 비중은 바로 직전 달의 비중을 활용하였고 예측된 머신러닝 모델의 경제 상황을 토대로 기존의 최적화 제약에 Rank 제약식을 추가하여 최적화된 자산 비중을 도출하였다. 더불어 최적화에 들어갈 수익률과 공분산 행렬은 투자자가 입력한 Lookback Period를 활용하여 Rebalancing하고자 하는 날짜의 최적 비중을 산정하여 배열로 통합하였다.
    
    ![image](https://user-images.githubusercontent.com/56333934/102777266-96acce80-43d3-11eb-8f79-3ea765c0048a.png)
    
  * Rebalancing을 반영한 BackTest table 생성
    - 투자기간에 해당하는 자산(‘Fama-French 5 Industry 또는 ’Fama-French 10 Industry‘)에 대하여 투자 기간에 해당하는 데이터프레임을 구성하였다. 투자자가 입력한 투자 금액의 자산군별 초기 금액은 투자금액 (초기비중으로 첫 투자 금액을 설정하였다.) 이후 아래 표와 같은 알고리즘으로 Rebalancing을 실시하여 Backtest를 진행하였다. Index를 3으로 나눴을 때 2가 남는 지점이 투자를 시작한 이후 각각 3개월, 6개월 등이 경과한 시점으로 Rebalancing이 실시되는 시점이라고 판단하여 해당하는 시점에 Rebalance를 하였다. 더불어 만약 투자 기간이 끝나는 시점과 Rebalance주기가 일치할 경우 이 시점에서는 Rebalancing을 할 필요가 없다고 판단하여 해당 시점의 경우 Rebalancing을 실시하지 않았다. 아래와 같은 알고리즘을 통해 1개월이 경과할 때마다 각 자산별 수익률만큼 이전 금액에서 곱해주되, 3개월마다 Rebalancing을 통해 조정하도록 설정하였다.
   
    ![image](https://user-images.githubusercontent.com/56333934/102777444-f1462a80-43d3-11eb-9156-548c74dd8374.png)
    
### UI
> 성과분석에는 총 6개의 그래프로 구성되어있다. 각 그래프는 Python 그래프 라이브러리 “plotly“를 사용하였으며 사용자가 입력한 값을 토대로 분석한 결과를 Html로 저장하여 보여준다. 벤치마크로는 1/N(Equally Weighted Portfolio)로 투자한 포트폴리오와 S&P500 지수를 사용하였다.
설정값: (투자성향: 중립형, 투자자산: Fama-French 10 Industry+Bond, 투자기간: 2000-01-2010-01, Lookback Period : 1년)

![image](https://user-images.githubusercontent.com/56333934/102778189-75e57880-43d5-11eb-8a7d-216499a192be.png)

### Maintainers
- 김성수 (경희대학교 산업경영공학과)
- 신시언 (경희대학교 산업경영공학과)

### Installation
> 프로그램 실행방법
  1. 모든 파일을 다운로드 받으세요
  2. 실행방법.txt를 읽으신 후 필요한 라이브러리 설치해주세요
  3. Optimize.ipynb를 차례대로 실행해주세요
  4. 로컬에 생성된 Result.html을 실행하시면 결과창을 보실 수 있습니다.
