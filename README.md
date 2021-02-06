# YBigta 학회 DA팀 2021 겨울방학 프로젝트
## Members
  * 김형준 Joon-Kim-Lang    
  * 최은솔   
  * 김지훈 Jeehoon-K 
# Seoul Apartment price prediction project

# About
  이 프로젝트는 연세대학교 빅데이터학회 Ybigta Data Analytics팀 2021년 겨울방학 프로젝트로,
  2008년부터 2020년까지의 아파트 거래정보 데이터를 활용하여 추후 가격을 예측하는 모델을 만들고
  장고 웹 프레임워크를 활용하여 사용자에게 가격예측 서비스를 제공하고 다양한 시각화 자료를
  제공함.   
     
  * Data origin :   
    * [2008~2017년 실거래가](https://dacon.io/competitions/official/21265/data/)   
    * [2017~2020년 실거래가](https://rt.molit.go.kr/)   
    * [공원 데이터](https://dacon.io/competitions/official/21265/data/)
  
# Overall Flow
![image](https://user-images.githubusercontent.com/61021101/106378798-ca274380-63ea-11eb-931a-56a303b5b3a6.png)

# Data Processing & Analysis
## 아파트 실거래가 분석모델
![image](https://user-images.githubusercontent.com/61021101/106378867-589bc500-63eb-11eb-970d-c880cc66b5ca.png)
* **data processing**   
  * 'transaction_day' : 'date(1\~10)','date(11\~20)','date(21~)'로 one-hot encoding   
  * 'dong','apt_name' : 'dong_enc','apt_name_enc'로 Label encoding   
  * 'price' : ex. 315,000 (object) -> 315000 (int)   
  * variable correlation : Nan (threshold : |0.2|)


![image](https://user-images.githubusercontent.com/61021101/106378868-5d607900-63eb-11eb-8cd6-350c5231d7f4.png)
* **model**   
  * LightGBM   
  * params = {"objective" : "regression", "metric" : "mse", 'n_estimators':15000,
              "num_leaves" : 20, "learning_rate" : 0.1, "bagging_fraction" : 0.8,
                'max_depth': 6}   
    lgb_model = lgb.train(params, train_ds, 1000, test_ds, verbose_eval=1000, early_stopping_rounds=100)
  * **RMSE score : 0.09477275477011567**   
     
* **function : price_pred(x1, x2,x3,x4, x5=77.95, x6=0,x7=0,x8=0,x9=9,x10=1998)**   
  * 'transaction_year' : x1, 'transaction_month' : x2, 'dong_enc' : x3, 'apt_name_enc' : x4, 'use_area(m2)' : x5, 'date(1\~10)' : x6, 'date(11\~20)' : x7, 'date(21~)' : x8, 'floor' : x9, 'year_found' : x10
## 아파트 주변 공원 시각화 모델 



# Backend Process

![image](https://user-images.githubusercontent.com/61021101/106378904-98fb4300-63eb-11eb-9d4f-0d1c3be15d13.png)

# Frontend Process

![image](https://user-images.githubusercontent.com/61021101/106378946-d790fd80-63eb-11eb-8be6-7c44502134d7.png)

# Result
![image](https://user-images.githubusercontent.com/61021101/106378988-2048b680-63ec-11eb-893d-4bca470a1197.png)

# Reference

