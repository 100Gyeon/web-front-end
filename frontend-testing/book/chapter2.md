# 2장. 테스트 방법과 테스트 전략

## 테스트 범위

웹 애플리케이션은 여러 모듈을 조합해 만든다.

```
1. 라이브러리가 제공하는 함수
2. 로직을 담당하는 함수
3. UI 관련 함수
4. 웹 API 클라이언트
5. API 서버
6. 데이터베이스 서버
```

테스트를 작성할 때는 어디부터 어디까지 커버하는 테스트인지 주의해야 한다.  
테스트 범위는 크게 4가지로 분류한다.

### 1. 정적 분석

- 타입스크립트나 ESLint가 제공하는 기능 활용

### 2. 단위 테스트

- 가장 기초적인 테스트
- **한 가지 모듈에 한정**하여 기능을 검증하는 테스트
- 테스트할 모듈이 특정 입력값을 받아 기대하는 출력값을 반환하는지 확인
- 독립된 환경에서 검증하기 때문에 실제 환경에서 거의 발생하지 않는 케이스(=코너 케이스) 검증에 적합

### 3. 통합 테스트

- **모듈 조합**으로 제공되는 기능을 검증하는 테스트
- 범위가 넓어질수록 효율적인 테스트가 가능하지만 상대적으로 대략적인 검증에 그치게 된다.
- `(1) 셀렉트 조작 -> (2) URL 검색 쿼리 변경 -> (3) API 호출 -> (4) 목록 화면 갱신` 과정에서 '(1)을 실행하면 (4)도 실행된다' 같은 테스트

### 4. E2E 테스트

- 가장 광범위한 테스트
- **실제 환경과 가장 유사**한 테스트
- 헤드리스 브라우저와 UI 자동화 도구를 결합하여 검증하는 테스트

## 테스트 목적

### 1. 기능 테스트 (인터랙션 테스트)

- 개발된 기능에 문제가 없는지 확인하는 테스트
- 대부분의 기능은 UI 컴포넌트 조작에서 시작하기 때문에 기능 테스트가 인터랙션 테스트가 될 때가 많다.

### 2. 비기능 테스트 (접근성 테스트)

- '키보드만으로 웹사이트를 이용할 수 있는가', '명암비가 시인성에 문제는 없는가'와 같은 다양한 검증 항목 존재

### 3. 시각적 회귀 테스트

- 특정 시점을 기준으로 전후 차이를 비교하는 테스트
- 헤드리스 브라우저에 그려진 내용을 캡처하여 캡처된 이미지 간 차이를 검증
- 초기 렌더링 상태만 비교하는 것에 그치지 않고, 사용자 조작으로 변경된 화면까지 캡처하여 비교

## 테스트 전략 모델

![테스트 범위와 비용의 상관관계](https://github.com/user-attachments/assets/9a691374-12db-4054-9246-3395787e4aaa)

위로 갈수록 실제 제품과 유사한 테스트가 가능하다.  
실제 제품과 유사한 테스트가 많을수록 좋은 전략으로 생각할 수 있으나, 환경을 구축하기 위해 많은 시간과 비용이 필요하다.  
테스트 계층 간 비용 분배는 테스트 전략을 세울 때 가장 중요한 검토 사항이다.  
비용 분배 최적화에 참고할 수 있는 테스트 전략 모델이 있다.

![테스트 전략 모델](https://github.com/user-attachments/assets/a8863d07-1870-40ca-9431-33df1c215814)

### 1. 아이스크림 콘 모델

- 상층부 테스트 비중이 높다.
- 안티패턴으로 자주 언급된다.
- 운용 비용이 높을 뿐만 아니라 외부 의존성 때문에 가끔씩 실패하는 불안정한 테스트가 비교적 많다.
- 브라우저를 포함하는 상층부 테스트는 실행 시간이 길어서 신속성이 떨어진다.

### 2. 피라미드 모델

- 하층부 테스트의 비중이 높을수록 더욱 안정적이고, 가성비 높은 테스트가 가능하다는 것이 핵심
- 하층부 테스트는 실행 시간이 짧아 신속성이 높고, 신속성이 높기 때문에 자주 실행할 수 있어 안정성도 높아진다.

### 3. 트로피 모델

- 통합 테스트 비중이 가장 높아야 한다는 것이 핵심이다.
- 사용자 조작을 기점으로 한 통합 테스트 비중이 높을수록 더욱 우수한 테스트 전략으로 본다.