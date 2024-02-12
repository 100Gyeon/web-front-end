### "use client"

- "use client"의 의미
  - "이 컴포넌트는 client에서 interactive 해야 해"
  - "이 컴포넌트는 hydrated 되어야 해"
- "use client"를 작성한 경우, HTML을 사용자에게 주고 나서 이벤트 리스너를 추가할 컴포넌트를 hydrate 함
  - "use client"는 오직 client에서만 render 된다는 것을 의미하지 않음
  - server에서 render 되고, frontend에서 hydrate 및 interactive 됨을 의미함
- "use client"를 작성하지 않으면 **서버 컴포넌트**
  - 서버 컴포넌트는 server에서 render 되고, hydrate 되지는 않음
  - 특정 컴포넌트는 hydrate 될 필요가 없음 (그냥 HTML로 남아있어도 상관없음)
  - 클라이언트에 딱 한 번만 render 되고 다시는 render 될 일이 없다면 사용 (ex. useState, onClick events 같은 것들이 없는 경우)
  - 사용자가 다운로드하는 JavaScript 양이 더 적음 -> 페이지 로딩 속도 빨라짐
  - 코드가 브라우저로 가지 않고 서버에서만 render 되니까 보안 신경쓰지 않고 코드에 API key 넣거나 DB와 통신 가능
- 클라이언트 컴포넌트 안에 서버 컴포넌트 가질 수 없음 (그 반대는 가능)

### 레이아웃 시스템

- app/layout.tsx 파일의 용도 : 복붙 없이 어디서나 요소 재사용 (ex. GNB, footer)
- Next.js는 layout component로 먼저 가서 export default function을 렌더링하고 URL을 확인
- 특정 페이지 폴더(ex. app/about-us)에서 특정 페이지만의 레이아웃 생성 가능