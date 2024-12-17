# angular-manual

1. Angular 应用是围绕组件构建的，组件是 Angular 的构建块。组件包含代码、HTML 布局和 CSS 样式信息，这些信息提供应用中元素的功能和外观。在 Angular 中，组件可以包含其他组件。应用的功能和外观可以划分并划分为组件。Angular apps are built around components, which are Angular's building blocks. `https://angular.dev/tutorials/first-app/02-HomeComponent`
2. Angular 使用 TypeScript 来充分利用强类型编程环境。强类型检查可降低应用中的一个元素向另一个元素发送格式错误的数据的可能性。此类类型不匹配错误会被 TypeScript 编译器捕获，许多此类错误也可以在您的 IDE 中捕获。`https://angular.dev/tutorials/first-app/04-interfaces`
3. `constructor` 是创建此组件时运行的第一个函数。The constructor is the first function that runs when this component is created. `https://angular.dev/tutorials/first-app/09-services`
```typescript
import { Component, inject } from '@angular/core';
import { HousingLocation } from "../housinglocation";
import { HousingService } from "../housing.service";

export class HomeComponent {
  housingLocationList: HousingLocation[] = [];
  housingService: HousingService = inject(HousingService);

  constructor() {
    this.housingLocationList = this.housingService.getAllHousingLocations();
  }
}
```
4. 
