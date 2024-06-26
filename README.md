# 야옹아 기부하개  
**URL** -> https://github.com/gibuhagae/gibuhagae  
**분류** -> 팀 프로젝트 (F-S 4명)  
**날짜** -> 2023.09.26 ~ 2023.10.20  
**환경** -> Spring(Boot, Security, Thymeleaf), MyBatis, Oracle  

![Untitled](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/01d0a30c-a5f9-4736-86b6-cdc39c79ccea)

## 소개
사회적.윤리적 성장 목표로 유기동물 보호 목적의 적립금 기부 시스템을 탑재한 반려동물 용품 쇼핑몰로써 상품 관리와 회원 시스템을 포함하고 있다.  

## 기능
![Untitled (1)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/3c381ea7-b057-4234-94a4-c64bb1eaf835)

**로그인 시스템**에서 Security Login System 커스텀마이징을 통한 로그인 구현, Security RememberMe를 사용한 로그인 유지, id 저장과 로그인 유지 설정 반영구 유지 기능, ID와 PWD 찾기 기능 구현

**회원가입, 회원정보**에서 정규식 처리를 통한 입력 조건 처리와 Daum API 연동을 통한 주소 입력, 그리고 ContextHolder에서 정보를 꺼내 회원정보 수정 구현

## 프로그램 개발
![Untitled (2)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/3820f3b8-a5c5-42f9-a757-a7ebc68210c4)

### 기획 과정(09.26 ~ 10.03)
![Untitled (3)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/0eb4dfbf-1022-450d-ad96-415ab72f7b96)  
<em> 위 그림은 gibuhagae 프로젝트 당시 Notion을 활용한 작업장이다. </em>

사전 조사 및 설계 단계로서 **1.프로젝트 주제 및 기능 분배 | 2.프로토타이핑.업무흐름도.ERD | 3.프로그램 목록 및 설계** 의 세 가지 단계로 분류 및 절차대로 수행해 나갔다. (1번 부분은 위에 설명을 했으므로 생략하고 2번 부분부터 시작하게 된다.)

![Untitled (4)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/e3b9a770-8592-4952-985c-0cde7418a35c)
<em> Figma, FigJam Tool을 활용하여 설계된 프로토타이핑과 순서도 </em>

각자 맡은 기능에 대한 요구 사항 명세서를 작성한 후, 이를 바탕으로 프로토타이핑과 순서도를 함께 도식화하였다. 이를 통해 빠르고 정확한 소통을 이끌어내고, 개발 환경에 산출물들을 바로 코드화하여 높은 생산성을 달성할 수 있었다.

![Untitled (5)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/d2757563-f2b1-4b93-ab5a-6598ed88078d)
<em> 요구사항 수집과 분석 및 개념적, 논리적 모델링 단계 과정을 거쳐 완성된 ERD </em>

프로젝트 주제와 기능 분배 이후에 각자의 기능에 대한 요구사항을 수집 및 분석한 후, 회의를 통해 개념적 데이터 모델링을 수행하였다. 이 과정에서 카디널리티 개념을 활용하여 모델링 연관관계를 구축 단계를 거쳐, 논리적 모델링을 위한 데이터 정형화 및 정규화 과정을 거쳤고, 마지막으로 물리적 모델링 단계에서 Oracle과 사상시켰다.

### 구현 기능(10.3 ~ 10.19)
![sub-gibuhagae drawio (2)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/c88f7a4d-4dc9-4e5b-a557-359c3c2ee733)
<em> 해당 프로젝트의 간략 설계도와 해당 주요 기능인 로그인 시스템에서 사용되는 Session 기술 메커니즘을 담고 있다. </em>

![Untitled (9)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/76afb01e-52e1-46bb-a8e2-ed460e5b2728)
<em> SpringSecurity System 메커니즘 과정에서 User Custom 구현 및 저장한 부분과 아이디 저장, 로그인 유지에 사용되는 쿠키 값들을 표시한 그림 </em>

#### Security Login 구현  
Spring Security UserDetailsService 인터페이스를 커스텀 구현하여 ContextHolder에 Entity Member 저장 처리

#### Login 유지 Remember Me
기존의 Session과 Cookie를 활용한 Security Remember-me를 사용하여 로그인 유지 기능을 구현할 수 있다고 판단, SecurityConfig 클래스의 @Bean 객체 컴포넌트인 filterChain에서 http.rememberMe()에 관련 메소드 부분들을 체인 연동 형식으로 커스터마이징하여 기능 구현

#### Checkbox의 id 저장과 Login 유지  
![Untitled (8)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/d01710ba-3397-4b6e-a469-b9252e3fe2f2)

쿠키 생성과 체크박스의 key=’id’를 LocalStorage에 저장하여 저장하여, 체크상자 상태를 반영구적으로 유지하게 만들고, 활성화된 상태에서는 기능이 수행되도록 처리

#### 아이디, 비밀번호 찾기 기능
![Untitled (7)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/ade47d3e-589a-4bed-84da-dc61e69b8569)

찾기 버튼 클릭 시 SecurityContextHolder에서 사용자 객체를 추출하여 데이터베이스에서 해당 사용자 정보를 확인, 정보가 있는지 여부에 따라 두 가지 경우로 나누어 처리. 정보가 없는 경우는 Modal Window 으로 알림 전달, 있는 경우는 ID와 임시 비밀번호를 발급하여 새 페이지에 표시하여 처리

#### 회원가입과 수정
![Untitled (6)](https://github.com/songbyhyeok/2023-HicodingGroupware/assets/63230518/9544728b-b1f2-46d9-9e95-c71ab5f826ef)

**회원가입**  
- 회원가입 시스템의 입력 조건은 유효성 검사 부분이 여러 개면서 동시에 복잡하여 오래 걸릴 것으로 판단, 이를 보완하기 위해 JavaScript 정규표현식을 통해 빠르게 처리할 것으로 고안하여 처리
- 주소 검색의 Modal Window 구현을 수동적으로 하는 것은 시간적으로 비효율적일 것으로 판단, 이를 주소 API 중 Daum 을 채택하여 구현

**회원가입 수정**  
- 확인이나 탈퇴 버튼을 누를 시 사용자 상태를 변경해야 하는 상황을 인지, 이를 SecurityContextHolder에서 사용자 정보를 꺼낼 수 있는 Principal 객체를 통해 가져와 쿼리를 통해 갱신

### 회고
#### 공정 단계
여태 배웠던 내용을 바탕으로 팀프로젝트를 진행한다고 했을 때 나름 긴장도 되고, 설레기도 했던 거 같다. 그래서 나름 단단히 각오를 하고 임하기로 했는데, 풀스택 교육 과정이라 그런지 기획 단계가 같이 포함되어 있어서 당황스러웠던 거 같다. 왜냐하면 짧은 시간에 제공된 체계적이고 정형화된 기획 시스템을 포함시켜야 했기 때문이다. 그래서 진행 중 주제에 대한 조사부터 시작해서 역할 분배 그리고 명세서 작성까지 마치며 서면의 노고가 느껴졌고, 제품에 대한 이해와 문서화 중요성 그리고 의사소통 기법까지 협업을 하면서 개발 외에 이런 점들도 정말 중요하다는 걸 느꼈고, 평소에 점 찍어둔 책 ‘로지컬 씽킹’을 읽고 언급한 중요한 역량들을 향상시켜보려고 한다.

#### 로그인 시스템
개발 과정 중 로그인 기능을 맡았던 점이 가장 잘한 선택 같았고, SpringSecurity 시스템 학습 및 로그인 관련 모듈 부분을 구현해서 회원 데이터를 저장 및 관리까지 개발 전에 우습게 보였는데, 보안도 껴있고 복잡한 구조로 구성되어 있어 흥미도 생기고 성취감도 많이 느꼈던 거 같다. 그리고 oauth 2.0 관련 api 로그인 구현을 가장 해보고 싶었는데 Session 방식을 선택했던 터라 할 수 없어 너무 아쉬웠다. 

#### 마무리
이것저것 배운 걸 다 활용하여 처음으로 B to C 개발을 해봤는데, 많은 것을 표현하지 못해서 솔직히 좀 아쉽기도 하고 많이 더 공부해야겠단 결심을 하게 된 경험이었다.
