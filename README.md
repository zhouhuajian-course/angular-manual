# angular-manual

https://angular.dev/  
https://github.com/angular/angular

组件、表单、路由、依赖注入、信号、延迟加载、Angular CLI、Angular DevTools、内置变量

双花括号`{{}}`——元素内容、方括号`[]`——元素属性、圆括号`()`——元素事件、"banana-in-a-box"`[()]`——双向绑定 Two-way binding、指令`*`directive

三个 Structural directives，v17之前`*ngFf`、`*ngFor`、`*ngSwitch`，v17之后可以使用`@if`、`@else`、`@for`、`@switch`进行替代，更直观，代码可读性更好

https://angularjs.org/ 这个网站不再维护，AngularJS 项目已被 Google 关闭，不再维护，老项目 AngularJS 已被 Google 新项目 Angular 替代   
https://angular.io/ 这个网站不再更新，大部分页面会自动跳转到 https://angular.dev/

In Angular, the `ng` stands for `Angular`. 

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
17. if else for
```html
<h1>User profile</h1>
@if (isAdmin()) {
  <h2>Admin settings</h2>
  <!-- ... -->
} @else {
  <h2>User settings</h2>
  <!-- ... -->  
}
<ul class="user-badge-list">
  @for (badge of badges(); track badge.id) {
    <li class="user-badge">{{badge.name}}</li>
  }
</ul>
```
18. Why is track in @for blocks important? `https://angular.dev/guide/templates/control-flow#why-is-track-in-for-blocks-important`
```text
为什么track区块@for很重要？
表达式track允许 Angular 维护数据与页面上的 DOM 节点之间的关系。这样，Angular 就可以在数据发生变化时执行最少的必要 DOM 操作来优化性能。

有效使用轨道可以显著提高应用程序在循环数据集合时的渲染性能。

选择唯一标识表达式中每个项目的属性track。如果您的数据模型包含唯一标识属性（通常为id或uuid），请使用此值。如果您的数据不包含这样的字段，强烈建议您添加一个。

对于永远不会改变的静态集合，您可以用它$index来告诉 Angular 通过集合中的索引来跟踪每个项目。

如果没有其他可用选项，您可以指定identity。这会告诉 Angular 使用三等号运算符 ( ===) 通过其引用标识跟踪项目。尽可能避免使用此选项，因为它可能会导致渲染更新速度明显变慢，因为 Angular 无法映射哪个数据项对应于哪些 DOM 节点。
```
19. Service 是可注入的可重用代码片段。当您需要在组件之间共享逻辑时，Angular 会利用依赖注入的设计模式，允许您创建一个“Service”，该Service允许您将代码注入组件，同时从单一真实来源进行管理。@Injectable 可被注入的
```typescript
import {Injectable} from '@angular/core';
@Injectable({providedIn: 'root'})
export class Calculator {
  add(x: number, y: number) {
    return x + y;
  }
}
```
```typescript
import { Component, inject } from '@angular/core';
import { Calculator } from './calculator';
@Component({
  selector: 'app-receipt',
  template: `<h1>The total is {{ totalCost }}</h1>`,
})
export class Receipt {
  private calculator = inject(Calculator);
  totalCost = this.calculator.add(50, 25);
}
```
20. RxJS 是一个库。它是基于观察者模式和流的响应式编程库，可以简化异步或回调的代码。
21. ng 命令 帮助文档
```
> ng --help
ng

Commands:
  ng add <collection>            Adds support for an external library to your project.
  ng analytics                   Configures the gathering of Angular CLI usage metrics.
                                 配置 收集 Angular CLI 使用数据 
  ng build [project]             Compiles an Angular application or library into an output directory named dist/ at
                                 the given output path.                                                   [aliases: b]
                                 编译一个angular应用或库到一个输出目录
  ng cache                       Configure persistent disk cache and retrieve cache statistics.
  ng completion                  Set up Angular CLI autocompletion for your terminal.
  ng config [json-path] [value]  Retrieves or sets Angular configuration values in the angular.json file for the
                                 workspace.
  ng deploy [project]            Invokes the deploy builder for a specified project or for the default project in the
                                 workspace.
  ng e2e [project]               Builds and serves an Angular application, then runs end-to-end tests.    [aliases: e]
                                 构建项目，启动服务器，然后运行端对端测试
  ng extract-i18n [project]      Extracts i18n messages from source code.
  ng generate                    Generates and/or modifies files based on a schematic.                    [aliases: g]
                                 生成或修改文件 [别名；g]
  ng lint [project]              Runs linting tools on Angular application code in a given project folder.
  ng new [name]                  Creates a new Angular workspace.                                         [aliases: n]
                                 创建一个新的 Angular 工作区 [别名：n]
  ng run <target>                Runs an Architect target with an optional custom builder configuration defined in
                                 your project.
  ng serve [project]             Builds and serves your application, rebuilding on file changes.     [aliases: dev, s]
                                 构建应用，并启动开发服务器，当文件修改，重新构建 [别名：dev, s]
  ng test [project]              Runs unit tests in a project.                                            [aliases: t]
                                 运行项目中的单元测试 [别名：t]
  ng update [packages..]         Updates your workspace and its dependencies. See https://update.angular.dev/.        
                                 更新你的工作区和它的依赖
  ng version                     Outputs Angular CLI version.                                             [aliases: v]
                                 输出 Angular 命令行工具 版本 [别名：v]

Options:
  --help     Shows a help message for this command in the console.                                           [boolean]
             在控制台显示这个命令的帮助信息
  --version  Show Angular CLI version.                                                                       [boolean]
             看 Angular 命令行工具 版本

For more information, see https://angular.dev/cli/.
```
22. ng generate --help
```
> ng generate --help
ng generate

Generates and/or modifies files based on a schematic.
生成或修改文件

Commands:
  ng generate <schematic>              Run the provided schematic.                                           [default]
  ng generate app-shell                Generates an application shell for running a server-side version of an app.    
  ng generate application [name]       Generates a new basic application definition in the "projects" subfolder of the
                                       workspace.                                                       [aliases: app]
                                       在工作区的projects子目录，生成一个新的基础的应用程序 [别名：app]
  ng generate class [name]             Creates a new, generic class definition in the given project.     [aliases: cl]
                                       在一个给定的项目里，创建一个新的通用的类 [别名：cl]
  ng generate component [name]         Creates a new, generic component definition in the given project.  [aliases: c]
                                       在一个给定的项目里，创建一个新的通用的组件 [别名：c]
  ng generate config [type]            Generates a configuration file in the given project.
                                       在一个给定的项目里，生成一个配置文件
  ng generate directive [name]         Creates a new, generic directive definition in the given project.  [aliases: d]
                                       在一个给定的项目里，创建一个新的通用的指令 [别名：d]
  ng generate enum [name]              Generates a new, generic enum definition in the given project.     [aliases: e]
                                       生成一个新的通用的枚举 [别名：e]
  ng generate environments             Generates and configures environment files for a project.
                                       生成并配置环境文件
  ng generate guard [name]             Generates a new, generic route guard definition in the given project.
                                                                                                          [aliases: g]
                                       创建一个新的通用的路由守卫 [别名：g]
  ng generate interceptor [name]       Creates a new, generic interceptor definition in the given project.
                                       创建一个新的通用的拦截器
  ng generate interface [name] [type]  Creates a new, generic interface definition in the given project.  [aliases: i]
                                       创建一个新的通用的接口 [别名：i]
                                       
  ng generate library [name]           Creates a new, generic library project in the current workspace. [aliases: lib]
                                       创建一个新的通用的库项目
  ng generate module [name]            Creates a new, generic NgModule definition in the given project.   [aliases: m]
                                       创建一个新的NgModule
  ng generate pipe [name]              Creates a new, generic pipe definition in the given project.       [aliases: p]
                                       创建一个新的管道
  ng generate resolver [name]          Generates a new, generic resolver definition in the given project. [aliases: r]
                                       创建一个新的
  ng generate service [name]           Creates a new, generic service definition in the given project.    [aliases: s]
                                       创建一个新的 service 服务
  ng generate service-worker           Pass this schematic to the "run" command to create a service worker
  ng generate web-worker [name]        Creates a new, generic web worker definition in the given project.

Arguments:
  schematic  The [collection:schematic] to run.                                                               [string]

Options:
      --help         Shows a help message for this command in the console.                                   [boolean]
      --interactive  Enable interactive input prompts.                                       [boolean] [default: true]
  -d, --dry-run      Run through and reports activity without writing out results.          [boolean] [default: false]
      --defaults     Disable interactive input prompts for options with a default.          [boolean] [default: false]
      --force        Force overwriting of existing files.                                   [boolean] [default: false]
```
23. ng new augular-app 一直回车，就是默认选项，Yes/No 回车，是 No
24. @Component 表明下面声明的类是一个组件
25. ng-template https://angular.dev/api/core/ng-template 
