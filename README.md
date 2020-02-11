# Node.js es6 and test cases

## nodejs에서 es6 사용
- ```$ npm install --save-dev @babel-cli @babel-preset-node6 @babel-register```
- Node v6에서 아직 지원하지 않는 module loader를 트랜스파일 해주기 위해 다음과 같이 .babelrc를 설정해준다.
  - ```$ vi .babelrc```
  - ```
     {
       "presets": ["@babel/preset-env"]
      }
  - package.json에서 스크립트 변경도 가능
  ```
  "scripts": {
    "test": "NODE_ENV=test npx mocha --require @babel/register --require @babel/polyfill --exec babel-node --exit ./test/**.spec.js",
    "start": "nodemon --exec babel-node app.js"
  }
  
## test with mocha, supertest, chai
- package.json의 scripts에서 마지막 ./test/**.spec.js로 작성되어있으면 test/example.spec.js로 테스트 디렉토리 및 스크립트 작성
```javascript
import request from "supertest";
import { expect } from "chai";
import Model from "../models/modelName";
import app from "../app";

describe("GET /" , () => {
  it("should world!", done => {
    request(app)
      .get("/")
      .expect(200)
      .end((err, res) => {
        if (err) {
          done(err);
          return;
         }
         expect(res.body).to.equal("world!")
         done();
       });
     });
   });
```
   
- 테스트 프레임워크는 mocha, Assertion 라이브러리는 chai, supertest로는 request를 보낸다.
