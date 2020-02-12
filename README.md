# Calculator
Calculating application with C++ MFC, Using class named calculator

### public 함수

```
enum {
		CALC_OP_UNKNOWN = 0,
		CALC_OP_PLUS = 1,
		CALC_OP_MINUS = 2,
		CALC_OP_MULTIPLY = 3,
		CALC_OP_DIVIDE = 4
	}; 
  enum { CALC_ERROR_UNKNOWN_OPERATION = 1, CALC_ERROR_DIV_BY_ZERO, CALC_ERROR_BAD_INPUT };
```

 연산자를 수식에 쓰기위해 임시적으로 int형으로 저장
 
 에러 및 unknown도 따로 저장
 
```
void SetQuestion(wstring question) { Initialize();  _question = question; };
```

* 연산 문장을 세팅합니다.

    - 입력값 : 연산문장 question(wstring)
    
    - 출력값 : 없음(void)
    
   + 작동 로직
    
        - Initialize()을 사용하여 내용을 초기화 합니다.
        
        - 초기화된 question에 입력값을 대입시킵니다.

```
double GetAnswer() { return _answer; };
```

* 출력하기위한 결과값을 받아옵니다.

    - 입력값 : 없음

    - 출력값 : 결과값(double)
    
   + 작동 로직
   
      - 실행시 결과값인 _answer를 리턴합니다.
```
int GetError() { return _errorCode; };
```

* 연산 결과의 성공 여부를 반환합니다.

  - 입력값 : 없음
  
  - 출력값 : 연산 결과(int)
  
  -작동 로직
  
    + errorCode 값을 리턴합니다.
    
    + 연산 성공시 0, 실패시 1, 그외 에러엔 기타 숫자 : 에러종류(ex. dib/0)값을 리턴합니다.

```
int GetLength() { return _length == 0 ? _question.length() : _length; }
```

* 연산한 항목의 길이를 리턴

    - 입력값 : 없음
  
    - 출력값 : 연산한 길이(Int);
    
   - 작동 로직
   
      - _length 값을 반환합니다.
      
      - _length 값은 연산 도중 parseQuestion() 함수의 작업이 끝나면 저장됩니다.
      
      - _length 값이 0이면 식 전체의 길이를 반환합니다.(아직 연산을 하지 않은 상태임)

```
void Initialize();
```

* 내용을 초기화합니다.

  - 입력값 : 없음
  
  - 출력값 : 없음(void)
  
 + 작동 로직
    
    - 작동시 question, vecNumber, vecOperators , answer, errorCode, length를 초기화합니다.

```
int Calculate();
```

* 기본 연산함수 

  - 입력값 : 없음
  
  - 출력값 : 연산 성공여부(int)
  
  + 작동 로직
  
      - 연산자 map currentOperators와 숫자 map currentNumbers를 읽습니다.
      
      - 연산자와 숫자를 하나씩 사용하여 다 사용할때까지 연산합니다.
      
      - 결과값은 _answer에 저장합니다.
      
      - 숫자 혹은 연산자가 남는경우 error 발생합니다.
  
      - 연산 성공시 0, 실패시 1 을 리턴합니다.


### protect 변수
```
	 wstring _question;
```
  * 연산문장을 넣는 변수
```
	double _answer;
```
  * 결과값을 넣는 변수
```
	vector<double> _vecNumbers; 
```
  * 각 항목 숫자를 넣는 벡터
```	
  vector<int> _vecOperators;
```  
  * 연산자를 저장하는 벡터
```
	int _errorCode;
```  
  * 연산 결과 성공여부 - 0:성공, 1:실패, 기타 숫자 : 에러 종류.(div/0 등)
```  
	int _length; 
```  
  * 연산한 문장 길이 체크용

### private 함수

```
  int calculate_Sub(map<int, wstring>& numbers, map<int, int>& operators); 
```

   * 3개의 항을 받아 연산하는 함수
   
        - 입력값 : 값 배열 numbers/ 연산자 배열 operators
        
        - 출력값 : 연산 성공여부(int)
        
      + 작동 로직
      
        - map 합수를 이용하여 numbers와 operators를 정의합니다.
      
        - 2개의 연산자와 3개의 값을 받아 연산합니다.
        
        - 2번째까지의 연산자중 *, / 가 있으면 그것을 우선, 아닌경우 순서대로 연산합니다.

        - 연산 성공시 0. 실패시 1 을 리턴한다.
        
        
```
	int calculate_Simple(double input1, double input2, int operation, double& result); 
```

  * 단순 두 항을 연산하는 함수
    
      - 입력값 : 계산되는수 input1, input2 / 연산자 operation / 결과값 result
        
      - 출력값 : 연산 성공여부(int)
        
      * 작동 로직
       
         - operation 값에 따라 input1 과 input2를 연산하고 결과값을 result에 저장합니다.
       
         - 연산 성공시 0, 실패시 1을 리턴한다.

```
	void setError(int errorCode) { _errorCode = errorCode; };
```

  * errorCode 를 세팅하는 함수
    
      - 입력값 : errorCode(int)
      
      - 출력값 : 없음(void)
      
     + 작동 로직
     
       - 입력받은 errorCode 값을 _errorCode에 저장합니다.
       
```
	int parseQuestion();
```

   * 문장을 값과 연산자로 구분
   
      - 입력값 : 없음
      
      - 출력값 : 숫자, 연산자
      
     + 작동 로직
     
        - 입력받은 숫자,연산자를 구분해서 저장합니다.
        
	- 연산자가 나올 때마다 _vecNumbers에 숫자를 _vecOperators에 연산자를 push back 합니다.
	
	- 문장의 길이를 length++ 를 이용해 기록합니다.
	
	-
