# FDA_project
## <금융데이터 분석 수업에서 진행한 기말 프로젝트>
> 최근 코로나19로 인한 전 세계적 팬데믹 현상과 더불어 4차 산업혁명 관련 기술의 발달로 인하여 노동시장에서의 불안정성이 커지고 저금리 기조가 지속되는 가운데 개인과 가계 단위의 투자자들이 재무 설계와 위험관리에 대한 관심이 점차 급증하고 있다. 투자자들은 점차 증가하는 불확실성 하에서 투자를 결정할 때 자신에게 가장 적합한 대안을 선택할 수 있어야 하며 투자자의 위험을 대하는 태도에 따른 투자 성향을 구분하여 투자 의사결정을 해야 한다. 특히, 주식시장에서 주식가격은 다양하고 불확실한 여러 요인에 의해 영향을 받기 때문에 주가변동의 이유를 정확하게 파악하는 것은 매우 어렵다. 하지만 주가를 결정하는 기업의 미래수익 및 할인율은 거시경제변수에 의해 영향을 받으므로 거시적인 관점에서 거시경제변수의 변동이 주가변동의 주요 요인이 될 수 있다. 이자율 기간구조에는 미래 경제상황에 대한 경제주체의 다양한 기대가 반영되어 있다. 특히 유동성이 높은 채권시장 거래에서 결정되는 장단기 이자율 격차인 이자율 스프레드는 시장참가자의 미래 지향적 기대가 잘 반영되어 있다. 따라서 본 연구는 실물경제 데이터인 GDP(Gross Domestic Product) 와 채권 Yeild Spread(U.S.10Year Treasury-Federal Funds Rate)를 통하여 미래 경제를 예측한 후 주식가격을 예측하여 개인의 투자성향에 따른 맞춤형 포트폴리오 제안을 목적으로 한다. 포트폴리오 최적화 시 개인 투자자의 투자 성향 뿐만 아니라 과거의 경제 상황의 산업군 별 수익률 순위와 거래 비용을 최소화하기 위한 Turn Over 제약을 추가하여 개인 투자자의 보다 효과적인 재무 설계와 위험관리를 하고자 하였다. 본 연구에서는 1960년부터 1999년까지의 실물경제 데이터와 금융데이터를 기계학습을 이용하여 훈련시켰으며 이후 2000년부터 2020년 10월까지를 Test 기간으로 설정하였다.

## Table of Contents
_Note: This is only a navigation guide for the specification, and does not define or mandate terms for any specification-compliant documents._

- [Sections](#sections)
  - [Data](#data)
  - [Modeling](#modeling)
  - [Algorithm](#algorithm)
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
  * 3달 후의 S&P500 수익률이 지난 30 
- 포트폴리오에 사용되는 자산 SET : Fama-french 5 industry, Fama-french 10 industry
- 투자성향 분석 : 투자성향에 관한 5가지 설문에 대해 4점 척도를 활용하여 투자자에게 맞는 투자성향을 산출하고자 하였다. `김지영, 2011`

### Modeling
![image](https://user-images.githubusercontent.com/56333934/102740610-9987cf00-4393-11eb-90f2-2f21052889ef.png)
- 각 모델 별로 Cross Validation 한 후 차이를 나타내는 표이다. Decision tree regressor의 평균과 분산이 다른 모델보다 우수한 성능을 보여주어 본 연구에서는 Decision Tree regressor 기법을 사용하여 모델링을 진행하였다. 해당 모델의 성능은 1960년부터 1999년 동안  트레이닝을 할 때의 정확도는 75% 였으나 2000년 이후의 데이터를 활용하여 예측을 했을 때의 정확도는 약 65% 다. 아래 그림에서 각 변수의 중요도를 확인할 수 있는데 본 연구에 사용된 모델에서 예측할 때 가장 중요한 변수는 yield spread 임을 알 수 있다.
![image](https://user-images.githubusercontent.com/56333934/102740610-9987cf00-4393-11eb-90f2-2f21052889ef.png)
- 아래 그림에선
- https://user-images.githubusercontent.com/56333934/102776640-703a6380-43d2-11eb-8b19-9368c8b90e2b.png

프로그램 실행방법
1. 모든 파일을 다운로드 받으세요
2. 실행방법.txt를 읽으신 후 필요한 라이브러리 설치해주세요
3. Optimize.ipynb를 차례대로 실행해주세요
4. 로컬에 생성된 Result.html을 실행하시면 결과창을 보실 수 있습니다.
