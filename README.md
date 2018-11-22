# ng-rxloop

## 安装

1. 在入口模块里引入 `RxloopModule`

```typescript
import { NgModule } from '@angular/core';
import { RxloopModule } from '@rxloop/store';
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

2. 定义 UserModel

```typescript
import { model, reducer, pipe } from '@rxloop/store';

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

3. 在业务组件之中
```typescript
import { Component } from '@angular/core';
import { Store } from '@rxloop/store';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.scss']
})
export class DatasourceComponent {
  constructor(private store: Store) { 

  }
  getUser() {
    this.store.dispatch({
      type: 'user/getUser',
      payload: 1,
    });
  }
}
```
