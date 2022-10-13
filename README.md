# **BMS 2.0 프론트엔드 프로젝트 리뷰**


## 1. 프로젝트 수행하고 나서 전체적인 느낌


- A 퍼블리셔 : 처음부터 온전히 투입된 첫 프로젝트여서 다음 공정에서 작업하기 편리하도록 소스를 구성하는데 어려움이 있었으나, 프로젝트를 진행하며 많이 배울 수 있었다.
- B 프론트개발자 : 퍼블리셔에서 프론트 개발자로 클래스 체인지 이후 첫 프로젝트로 기술적(React)인 어려움에 파트 PL로서의 역할적인 어려움이 가중되어 부담이 있었지만 그만큼 성취감도 있었다.
- C 퍼블리셔 : 프론트 가이드부터 주도적으로 진행해본 경험이 처음이어서 재미있었고 실력도 늘었지만, 팀간 및 수행사,고객사간 협의 또는 협업에 어려움이 있었다.
- D 프론트개발자 : 프론트엔드 전담 개발이 처음이어서 기대가 컸으나,프로젝트 데이터 구조가 예상 외로 복잡하여 시행착오를 겪었다.


##  2. 개발 환경 리뷰


1. #### MacOS

    - 사용 6개월만에 전반적으로 익숙해져서 프로젝트를 수행하는데에 큰 어려움은 없었다.
    - Homebrew를 통한 개발&테스트 환경 표준화에 이점이 있었다.
    - Intel Mac 사용자를 위한 고려사항이 일부 필요했다.


2. #### Chrome

    - 다음 프로젝트에서는 Chrome 개발자 도구 소스 탭의 breakpoint를 통해 디버깅이 가능한 환경을 구성했으면 좋겠다.


3. #### Teams

    - 스토리보드, 일정 문서 등을 공유하기 위해 팀즈 파일 저장소(OneDrive)를 사용했다.
    - Gantt Chart<sup id="gantt-chart">[1](#gantt-chart)</sup> 지원 도구(Notion 등)를 도입하는것에 대한 추가적인 검토와 검증이 필요하다.

4. #### Git

    - fetch / pull, commit / push 등 기본적 사이클에 대한 이해도가 높아져서 큰 충돌이나 소스 손실이 눈에 띄게 발생하지는 않았다.
    - 프로젝트 참여자 전체를 대상으로 branch naming guideline 확립 및 교육이 필요하다.
    - Pull Request / Frequent Source Review - Github, Gitlab, Bitbucket 등등 Git 저장소 시스템의 확장 기능 사용성 확대 필요에 대비해야한다.
      -> pilot 한번쯤 시도


5. #### Postman

    - Backend API의 테스트 (FE측, BE측 모두) 에 활용성이 좋았다.
    - Postman<sup>[2](#postman)</sup>의 대체로 Swagger UI를 사용하는게 더 편리할 것 같다고 생각하지만 실제 백엔드 개발자의 공수가 투입되어야 하는 만큼 그들이 익숙한 툴을 사용하는 것도 중요 고려사항인 것 같다.
    - Swagger UI<sup>[3](#swagger-ui)</sup>를 사용한 pilot 프로젝트를 수행해서 얼마나 사용성이 좋은지 서로 확인하는 기회를 가지는 것도 좋을 것 같다.


6. #### Figma

    - Zeplin, XD 비교하여 Figma에는 최근 변경사항에 대해 확인할 수 있는 방법이 부족하여 실질적으로 작업자간 소통 없이 툴 자체만으로 변경사항을 인지하기가 힘들다.
    - 코멘트를 달 수 있는 기능은 편했다. -> 작업자간 소통을 보조할 수 있는 기능으로서는 좋았으나 이 역시 수정시 자동으로 작성되는 것이 아닌 일부러 공수를 투입해야 하는 기능이어서 부담되는 부분이 있다.


7. #### Webstorm

    - Git lifecycle 지원하는 여러가지 플러그인 등 기능이 좋았다.
    - BMS 프로젝트에서는 ESLint<sup>[4](#eslint)</sup>를 사용하지 않았지만 향후 프로젝트에는 ESLint, 가능하다면 Prettier도 사용할 예정이므로 대비가 필요하다.


8. #### Spring 프로젝트 하위 워크스페이스 구조 - React build 공정

    - 선택의 영역이 아니었다. -> 단일 서버 인스턴스 요구사항 때문에 어쩔 수 없던 점.
    - 현재 방식의 장점 : 서버 구성 등을 신경쓸 필요가 없었다. 백엔드+프론트엔드 통합 세션을 구성할 수 있다.
    - 현재 방식의 단점 : 세부적 문제 발생에 대응하기 어렵다. 프론트 빌드만 따로 하는 방법 등 자원 낭비를 줄이는 방법을 추가로 마련해야 했으나 미비했다.
    - 현재 방식을 사용하지 않을 경우 장점 : 백엔드 서비스가 노출되지 않아 보안에 장점이 있고, 단독 빌드 등 자유도 높다.
    - 현재 방식을 사용하지 않을 경우 단점 : 인스턴스 추가 필요 및 책임 소지가 발생하는 부분 등이 있다.
    - 향후 프로젝트에는 구현 전단계 설계 공정에서 프론트엔드 엔지니어가 적극적으로 참여하여 CI/CD 구성(POM.xml이 아닌 Jenkins에서 직접 shell을 통해 yarn build 실행 등)에까지 영향력을 행사할 수 있도록 하는것이 희망사항이다.
    - Docker를 활용한 표준 아키텍쳐를 구성하여 이를 고객사에 제안 및 드라이브하는 방법도 고려가 필요하다.





##  3. Dependency 리뷰


1. #### React

    - useState, useEffect, useRef 등 기본적 lifecycle에 대한 이해도가 증진했다.

    - React 자체적인 사용에 대한 어려움 보다는 각종 dependency의 사용법 숙지에 관한 어려움이 많은 것으로 보인다.


2. #### Vite + SASS

    - 속도와 설정이 빠르다.

    - RISK : 많은 webpack 확장 기능들이 vite를 지원할지 여부를 항상 확인해야 한다. -> 점점 개선되고 있지만 vite의 사용률이 webpack을 역전하기 전까지는 항상 risk


3. #### Bootstrap

    - 퍼블 입장에선 어렵지 않았고, 개발 입장에선 CSS를 직접 만지지 않아도 되어서 편하다.

    - 부트스트랩에서 제공하는 클래스명을 기억하기가 어려워 반드시 IDE의 보조를 받아야 한다.

    - 90%의 수요가 선정의된 스타일이었으나 나머지 10%의 예외의 경우 CSS 등에 접근하기가 어렵다. (CSS 파일이 산발적으로 워크스페이스 내에 흩어지는 결과 발생)

    - Tailwind CSS 검토를 고려해보면 좋을 것 같다.


4. #### dayjs<sup>[5](#day-js)</sup>

    - moment.js의 지원 중단으로 프로젝트 중간에 대체했다.

    - Timezone 계산, 시간 객체간 비교&계산&변환, formatting에 유리하다.

    - 차트 drill up/down<sup>[6](#drill-updown)</sup>에 시간 단위 계산에 필수적이었다.


5. #### just-safe-get / just-safe-set

    - json-helper를 확장해서 사용 -> 개발자들에게 공유해서 방법론 통일을 위한 시도가 필요하다.

    - data API parsing, validation 등에 사용했다.


6. #### rc-tree ❌

    - 태블릿에서 드래그/드랍 동작하지 않는 이슈 - js 추가 로딩으로 해결했다.

      ```html
      <script id="DragDropTouch" src="/assets/js/dragDropTouch/dragDropTouch.js"></script>
      ```

    - 콘솔에 알 수 없는 warning 발생 - callback 함수 안과 밖의 파라미터명 충돌로 인한 오류였다.
    - 스타일링 제한이 있었다.
    - 다음 프로젝트에서는 자체적으로 Tree 컴포넌트를 개발하여 반영할 수 있도록 시도하는 것이 나을 것으로 소견된다.


7. #### chart.js<sup>[7](#chart-js)</sup>

    - 드릴 업/다운시 좌표 인식에 대한 버그 - padding 인위적 추가로 해결했다.


8. #### react-dnd<sup>[8](#react-dnd)</sup>

    - 태블릿에서 드래그/드랍 동작하지 않는 이슈 -> backend(드래그&드랍 엔진 HTML5 + Touch >> Multibackend ) 교체로 일부 해결했으나 preview 기능이 안드로이드에서는 동작하지 않았다.
    - preview 기능이 안드로이드 태블릿에서 동작할 수 있는 추가 dependency로 react-dnd-preview를 사용했다.


9. #### react-hook-form

    - 대안적 dependency -> Formik
    - 가장 어려웠던 점 : 사용자 액션을 통해 값을 변경해도 반영되어 받아지지 않고, 기본값을 지정해도 표출되지 않고, isValid/isDirty<sup>[9](#isvalid-isdirty)</sup>가 즉각적으로 반영되지 않는 점
    - 중간에 디자인 변경으로 재작업이 발생한 점, 데이터를 뒤늦게 반영하여 확인 시점이 늦어진 점 등이 hazard로 작용했다.
    - 다음 프로젝트부터는 general-input의 설계만 계승해서 새로운 코드로 신규 작성하여 사용하고 Row/Col 디자인을 배제하고 인풋 고유의 기능만 제공하는 컴포넌트로 개발하는게 좋을 것 같다.
    - 화면 코드에 Controller를 사용하지 않도록 공통 컴포넌트에 통합개발


10. #### i18next, react-i18next

    - useTranslation >> useI18n으로 확장하여 사용 - 전반적으로 편했다.

    ```javascript
    const {g, t} = useI18n('review.design');
    g('common.all');
    t('review-title');
    ```

    - JSON 형태로 소스가 나가서 번역되어 재적용하는 부분에 어려움이 있었는지 번역 파트의 피드백 수집 필요하다.
    - getPostposition 함수를 사용하여 한글 받침 여부에 따라 조사(은/는, 을/를, 이/가 등)를 구별해서 사용하는 유틸리티를 적극적으로 재사용해볼 필요가 있다.


11. #### Redux

    - persist store 설계 검토 방법론 수립 (어느 스토어는 필요할지, 어느 스토어는 불필요할지 결정)


12. #### react-router-dom

    - 리디렉션 할때

     ```javascript
     const navigate = useNavigate();
     navigate.navigate('/review/complete/detail', {replace: true});	// {replace: true} 안쓰는걸 권장 - {replace: true}가 있으면 history가 쌓이지 않음
     ```


13. #### react-vertical-timeline-component

    - 리뷰 -> 코멘트 말풍선 목록 컴포넌트
    - 예상외로 잘 다듬어져 나온 컴포넌트로 가성비 최고였다.


14. #### scoped CSS

    - 해당 컴포넌트 하위에만 영향을 미칠 수 있도록 제한하는 기능이 필요하다.
    - CSS파일이 산발적으로 여기저기 흩어지는 단점을 극복하기 위한 대안이 필요하다.


15. #### Summernote ❗️

    - 이 기능을 지원하기 위해서 React 애플리케이션에 jQuery를 적용했다.
    - jQuery를 통해 textarea를 summernote로 변환하며, 이 변환을 자동화하는 데에 React 컴포넌트를 사용했다.
    - Bootstrap 중복(심지어 다른 버전) 로드되는 risk가 있다.
    - 자체적 개발로 display 기능까지는 구현 가능하나 editor 기능 구현은 많은시간이 필요하다.
    - 현재로선 대체제가 없다.


16. #### Soyuz template

    - 구현에 사용하지 않았다.(요구 기능에 합치하는 테마가 아니었고, React로 제작되지도 않았으며, 요구사항이 각 화면마다 약간씩 다름.)
    - 제안시 고객사에는 환상을 심어주었으나 실제 개발에는 도움이 되지 않아 요구사항과 구현사항의 간극을 발생시킬 전형적인 vaporware였다.





## 4. 자체 개발 공통&확장 코드 / 컴포넌트 리뷰


(♻️ 표시는 향후 재사용을 위한 리패키징 대상)

1. #### 아키텍쳐, 워크스페이스 폴더 구조

    - 타입스크립트 사용 희망 -> 궁극적으로 지향해야 하는 점은 인정하지만 최근 입문자 비율이 높은 현재 상황을 감안하면 최소 올해는 타입스크립트 설계를 지양한다.

    - forms / sf-by ... 폴더구조와 register / .... 폴더구조의 mismatch -> 설계 fault


2. #### 업로드/다운로드 컴포넌트 ♻️

    - react-hook-form에서 입출력하는 onChange, field.value 등을 지원할 수 있도록 확장이 필요하다. (입출력 변수 표준화)
    - 항상 화면 개발할 때 업로드 연동 부분은 1차적으로 다음 코드 적용 후 개발, 즉 특정 사원의 디펜던시가 컸다고 보인다.

   ```javascript
   // TODO : 업로드 연동은 특정 사원 지원 받아 적용
   ```

    - React 애플리케이션에서 사용하는 컴포넌트 외에도 별도 애플리케이션 빌드를 통해 F/E에서 사용하는 Fork 존재 -> 둘 간극이 점점 넓어질 것으로 예상되며 통합할 수 있는지 검토가 필요하다.
    - 컴포넌트를 처음 접하는 개발자도 위 TODO 주석 단계를 건너뛸 수 있도록 상세한 가이드 문서(Mark Down)를 작성하는 절차가 필요하다.


3. #### 모달 메세지 팝업

    - 복붙으로 해결할 수 있었다.

    - Bootstrap 컴포넌트를 사용하여 편리했던 점중에 하나다.


4. #### 표준 API 연동 구조 (api-helper / bms-api-helper) ♻️

    - currentPath을 기반으로 호출 및 저장하는 컨셉이 편리했다.
    - navigate 등 화면 이동시 이전 화면의 데이터를 날리는 등의 추가 확장이 필요하다.
    - bms-api-helper를 조금 더 간소화할 수 있지 않았나 하는 아쉬움이 남았다.


5. #### DataTable ♻️

    - 체크/라디오 등 지원, rowSpan 헤드 등 지원 및 pagenation 표준화 적용한 테이블 컴포넌트이다.
    - 엑셀 import/export 기능 추가에 대한 검토가 필요하다.
    - 상세 적용 가이드를 만들어야 한다.


6. #### GeneralInput ♻️

    - 위 react-hook-form에 통합 작성함


7. #### 바, 도넛, 라인, 드릴라인 그래프

    - 객체지향 구현시 interface 등 TypeScript를 통한 이점 활용이 기대된다.


8. #### data-helper, menu-helper, biz-helper, view-helper

    - 옛날에는 CommonUtil.js, _util.js ... 이런 이름으로 모든 기능, 계산, 비즈니스로직 관련 유틸리티 함수를 때려넣는 방식을 많이 썼으나, 목적에 맞게 세분화하려고 각 기능별 helper라는 명명규칙을 사용했다.

    - 프로젝트 경험에 따라 향후에도 불필요한 항목 배제하고 필요항목은 추가해야한다.


9. #### 페이지 목록

    - 일정 관리의 이원화, 일정 기입에 대한 추가 공수가 발생했다.

    - 페이지 목록에 일정을 기입하는 것은 향후부터는 지양해야 할 것 같다.



## 5. 기타 개선할 점


1. #### PMO, 기획 협업간 개선 사항

    - 보고용 일정, 내부용 일정으로 분리해 진행하여 납기가 임박했을 때 실제 구현과 납기 사이의 간극이 발생했다.
    - QA에서 오류가 발생한 케이스에 대하여 어떤 조회 항목 정보 등의 상세 데이터 제공이 부족했다.
    - 현행화가 더디게 된 점 -> 스토리보드 변경 발생시 변경된 부분만 정확하게 확인할 수 없어 불편함이 있었다.


2. #### 디자인 협업간 개선 사항

    -  디자인 변경점 추적이 어려운 툴(Figma)을 사용하였으나 이를 보완하기 위한 방법론적 노력이 부족했다.
    -  디자인 가이드 변경점에 대한 공유가 즉각적이지 못하고 현행화가 이루어지지 않으며 일부 페이지에만 변경된 가이드가 반영되어 가이드 분리 적용 여부를 따로 확인해야했던 점이 불편했다.


3. #### 백엔드 협업간 개선 사항

    - 백엔드 엔지니어들도 decoupled 아키텍쳐 개발에 대한 경험이 부족하여 서로 가이드를 많이 주고 받는 것이 앞으로도 필요할 것으로 보인다.


4. #### 기타

    - 프로젝트 리뷰를 함으로써 차후 프로젝트가 더 수월하게 진행될 것 같아 앞으로도 프로젝트 수행시마다 리뷰를 하면 좋을 것 같다.
    - 향후 프로젝트 리뷰 방법론에 대해 대상 및 범위 정하여 관습적으로 지속되기를 희망한다.


<br>

------
<a name="gantt-chart" href="#gantt-chart">1</a>: 프로젝트 일정관리를 위한 바형태의 도구<br>
<a name="postman" href="#postman">2</a>: API 개발을 빠르고 쉽게 구현할수있도록 도와주며 개발된 API를 테스트하여 공유할수있도록 도와주는 플랫폼<br>
<a name="swagger-ui" href="#swagger-ui">3</a>: 사용자가 REST API를 빠르고 쉽게 배우고 실행하도록 하기 위해 대화식 API 콘솔을 생성할 수 있는 표시장치 프레임워크<br>
<a name="eslint" href="#eslint">4</a>: 코드를 분석해 문법적인 오류나 안티 패턴을 찾아주고 일관된 코드 스타일로 작성하도록 도와주는 오픈소스<br>
<a name="day-js" href="#day-js">5</a>: 많은 JavaScript 날짜 관련 라이브러리중 가장 가벼운 라이브러리<br>
<a name="drill-updown" href="#drill-updown">6</a>: <br/>드릴다운(Drill Down)데이터 조회를 상위 수준에서 하위 수준으로 하는 방식을 의미합니다.<br>드릴업(Drill Up)데이터 조회를 하위 수준에서 상위 수준으로 하는 방식을 의미합니다.<br>
<a name="chart-js" href="#chart-js">7</a>: 막대 그래프, 차트등 데이터 시각화를위한 오픈소스 라이브러리 <br>
<a name="react-dnd" href="#react-dnd">8</a>: 아이템간의 순서변경, 드래그 액션을 편리하게 사용할수있는 기능<br>
<a name="isvalid-isdirty" href="#isvalid-isdirty">9</a>: useForm에 어떤 필드든 특정 이벤트(사용자의 입력등)가 있었는지 확인할때사용 어떤 필드에 사용자 입력이 있었는지 알아낼때 사용


   
