# angular-manual

https://angular.dev/  
https://github.com/angular/angular

组件、表单、路由、依赖注入、信号、延迟加载、Angular CLI、Angular DevTools、内置变量

双花括号`{{}}`——元素内容、方括号`[]`——元素属性、圆括号`()`——元素事件

`@if`、`@for`

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

  constructor() {。
    this.housingLocationList = this.housingService.getAllHousingLocations();
  }
}
```
4. 服务端渲染 Server-Side Rendering (SSR) `https://angular.dev/guide/ssr`
5. Static Site Generation (SSG/Prerendering) `https://angular.dev/guide/prerendering`
6. `angular.json` 叫 Angular 工作区配置 `Angular workspace configuration` `https://angular.dev/reference/configs/workspace-config#alternate-build-configurations.`
7. `{{ housingLocation?.name }}` `https://angular.dev/tutorials/first-app/11-details-page` Notice that the housingLocation properties are being accessed with the optional chaining operator ?. This ensures that if the housingLocation value is null or undefined the application doesn't crash.
8. `In Angular, FormGroup and FormControl are types that enable you to build forms. The FormControl type can provide a default value and shape the form data.` `https://angular.dev/tutorials/first-app/12-forms`
9. `this.applyForm.value.firstName ?? ''` 空值合并运算符 （??）是一个逻辑运算符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数。 `https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing` ` In the above code, the FormControls may return null. This code uses the nullish coalescing operator to default to empty string if the value is null.` `https://angular.dev/tutorials/first-app/12-forms`
10.  Angular Language Service 扩展 语言服务扩展 VS Code。Angular 语言服务为代码编辑器提供了一种在 Angular 模板内获取补全、错误、提示和导航的方法。它适用于单独 HTML 文件中的外部模板，也适用于内联模板。https://angular.dev/tools/language-service#visual-studio-code
11. 组件 是 Angular 应用程序 主要的构建块 Components are the main building blocks of Angular applications. Each component represents a part of a larger web page. Organizing an application into components helps provide structure to your project, clearly separating code into specific parts that are easy to maintain and grow over time.
12. 信号 一个信号是一个value的轻量级包装器。 In Angular, you use signals to create and manage state. A signal is a lightweight wrapper around a value. 
```javascript
// node test.mjs
import { signal } from "@angular/core";

const firstName =  signal('Mrogan')
console.log(firstName());

firstName.set("Jaime")
console.log(firstName());

firstName.update(name => name.toUpperCase())
console.log(firstName());

// Mrogan
// Jaime
// JAIME
```
13. Angular 用信号来实现 响应式 Angular tracks where signals are read and when they're updated. The framework uses this information to do additional work, such as updating the DOM with new state. This ability to respond to changing signal values over time is known as reactivity. 
14. 即使没有使用信号，修改组件属性，也能响应式，页面也会更新。用信号的方式也可以。
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `Test!Test!{{name}}`
})
export class AppComponent {
  name: string;
  constructor() {
    this.name = "test"
    const appComponent = this
    setTimeout(() => {
      appComponent.name = "test!test!"
    }, 3000);
  }
}
// 3秒后 页面显示 Test!Test!test!test!
```
```typescript
import { Component, Signal, signal } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `Test!Test!{{name()}}`
})
export class AppComponent {
  name: any;
  constructor() {
    this.name = signal("test")
    const appComponent = this
    setTimeout(() => {
      appComponent.name.set("test!test!")
    }, 3000);
  }
}
// 3秒后 页面显示 Test!Test!test!test!
```
15. DOM元素属性动态绑定 You can also bind to HTML attributes by prefixing the attribute name with attr.:
```html
<!-- Bind the `role` attribute on the `<ul>` element to value of `listRole`. -->
<ul [attr.role]="listRole()">
```
16. 时间处理 拿 event 对象 If you need to pass the event object to your listener, you can use Angular's built-in $event variable inside the function call:
```typescript
@Component({
  /*...*/
  // Add an 'click' event handler that calls the `cancelSubscription` method. 
  template: `<button (click)="cancelSubscription($event)">Cancel subscription</button>`,
})
export class UserProfile {
  /* ... */
  
  cancelSubscription(event: Event) { /* Your event handling code goes here. */  }
}
```