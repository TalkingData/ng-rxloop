# ng-rxloop
状态：设计阶段草案，相关 api 待讨论。

## 安装
1. 通过 npm 安装
```bash
$ npm i ng-rxloop
```

2. 在入口模块里引入 `RxloopModule`

```typescript
import { NgModule } from '@angular/core';
import { RxloopModule } from 'ng-rxloop';
import { UserModel, DatasetModel, ProjectModel } from './models';
​
@NgModule({
  imports: [
    RxloopModule.forRoot([
      UserModel,
      DatasetModel,
      ProjectModel,
    ])
  ]
})
export class AppModule {}
```

3. 定义 UserModel

```typescript
import { model, reducer, pipe } from 'ng-rxloop';

@model({
  a: 1,
  b: 2,
  c: 3,
})
export class User {
  constructor(private userService: UserService) {}

  @reducer
  info(state) { return state }

  @reducer
  info2(state) { return state }

  @pipe
  getUser(action$, { map, dispatch }) {
    return action$;
  }

  @pipe
  getData2(action$, { map, dispatch }) {
    return action$;
  }
}
```

4. 定义 Action

```typescript
export class GetUserAction {
  readonly type: string = 'user/getUser';
  constructor(private id: string) {
    this.payload = id
  }
}
```

5. 在业务组件之中
```typescript
import { Component } from '@angular/core';
import { Store } from 'ng-rxloop';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.scss']
})
export class DatasourceComponent {
  constructor(private store: Store) {}
  getUser() {
    this.store.dispatch({
      type: 'user/getUser',
      payload: 1,
    });
    // 或者通过 new Action 的方式
    // this.store.dispatch(new GetUserAction(1));
  }
}
```

