# angular-manual

https://angular.dev/  
https://github.com/angular/angular

HTML标签尖括号 `<>` 叫做 `Angular Brackets` 或者 `Angle Brackets`，这是 `Angular` 名字的由来，为了扩展 HTML。

指令 directives 可以扩展 HTML 标签和 HTML 属性。

Directives are classes that add additional behavior to elements in your Angular applications. 

指令是一些类，这些类在你的应用程序中 给 元素 添加额外的行为。

`@angular/core` `@angular/common` ... 这些都是一些 `Angular` npm 包，不同的包里面，会把不同的功能聚在一起。

模块 Module 把 一些组件、指令、管道 整合在一起。可以把庞大的功能分成一个一个划分清晰的模块，例如按业务不同，划分模块。

Angular DevTools https://angular.dev/tools/devtools#

CSS 扩展语言

`GetAngular` -> `AngularJS` (script 标签 src ../angular.js) -> `Angular`

`filter` -> `pipe` 

组件、表单、路由、依赖注入、信号、延迟加载、Angular CLI、Angular DevTools、内置变量

双花括号`{{}}`——元素内容、元素属性值 文本插值（语法）、方括号`[]`——元素属性、圆括号`()`——元素事件、"banana-in-a-box"`[()]`——双向绑定 Two-way binding、指令`*`directive

三个 Structural directives，v17之前`*ngFf`、`*ngFor`、`*ngSwitch`，v17之后可以使用`@if`、`@else`、`@for`、`@switch`进行替代，更直观，代码可读性更好

https://angularjs.org/ 这个网站不再维护，AngularJS 项目已被 Google 关闭，不再维护，老项目 AngularJS 已被 Google 新项目 Angular 替代   
https://angular.io/ 这个网站不再更新，大部分页面会自动跳转到 https://angular.dev/

In Angular, the `ng` stands for `Angular`. 

`<app-root></app-root>` 这种元素，就是一个Angular组件（实例）。`When an element is an Angular component, ...`

Angular 单页应用 SPA 不会重复加载 页面，非常节省网站流量，有更快的加载速度，非常给力。

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
26. 组件包含代码、HTML布局、CSS样式信息，提供一个元素的功能和外观。在Angular 组件可以包含其他组件。一个应用程序的功能和外观能够被分离到不同的组件中。Components contain the code, HTML layout, and CSS style information that provide the function and appearance of an element in the app. In Angular, components can contain other components. An app's functions and appearance can be divided and partitioned into components.
27. In Angular, components have metadata that define its properties.
28. 组件可以使用 使用 input 属性 来接收数据 https://angular.dev/guide/components/inputs `Accepting data with input properties`
29. When you use a component, you commonly want to pass some data to it. A component specifies the data that it accepts by declaring inputs:
```typescript
import {Component, input} from '@angular/core';
@Component({/*...*/})
export class CustomSlider {
  // Declare an input named 'value' with a default value of zero.
  // 0是默认值
  value = input(0);
}
```
This lets you bind to the property in a template:  
和模板中的元素属性进行绑定
```html
<custom-slider [value]="50" />
```
If an input has a default value, TypeScript infers the type from the default value:  
如果一个input有默认值，TS会根据默认值推断数据类型
```typescript
@Component({/*...*/})
export class CustomSlider {
  // TypeScript infers that this input is a number, returning InputSignal<number>.
  value = input(0);
}
```
You can explicitly declare a type for the input by specifying a generic parameter to the function.  
你可以显式给input声明给类型，通过给函数指定一个泛型参数  
If an input without a default value is not set, its value is undefined:  
如果一个input没有设置默认值，它的值是undefined  
```typescript
@Component({/*...*/})
export class CustomSlider {
  // Produces an InputSignal<number | undefined> because `value` may not be set.
  value = input<number>();
}
```
Angular records inputs statically at compile-time. Inputs cannot be added or removed at run-time.  
Angular 在编译期，静态地记录 inputs。Inputs 不能在运行期被添加或移除。  
The input function has special meaning to the Angular compiler. You can exclusively call input in component and directive property initializers.  
When extending a component class, inputs are inherited by the child class.  
当继承一个组件类，inputs会被子类继承  
Input names are case-sensitive.  
input名是区分大小写的。
30. 组件的input可以使用 input() 或 @Input，使用方式会有些不同，但都可以实现功能。
31. 两种input，基于信号的input和基于装饰器的input。数据绑定方式。Binding to an input is the same in both signal-based and decorator-based inputs:
```html
<custom-slider [value]="50" />
```
32. an input是单向数据绑定，a model input是双向数据绑定？
33. 双向数据绑定例子
```text
App 500
Home Joe 50 有多少钱 500
```
```typescript
import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';
import { HomeComponent } from "./home/home.component";

@Component({
  selector: 'app-root',
  imports: [HomeComponent],
  // templateUrl: './app.component.html',
  template: `App {{stuMoney}} <br/>
  <app-home [age]="50" [name]="stuName" [(money)]="stuMoney"></app-home>`,
  // styleUrl: './app.component.css'
})
export class AppComponent {
  title = 'angular-app';
  stuName = 'Joe';
  stuMoney = 800
}
```
```typescript
import { Component, Input, input, model } from '@angular/core';

@Component({
  selector: 'app-home',
  imports: [],
  template: "Home {{ name }} {{ age() }} 有多少钱 {{ money() }}",
  styleUrl: './home.component.css'
})
export class HomeComponent {
  @Input()
  name = "Trump"
  age = input(18)
  money = model(0)
  constructor() {
    setTimeout(() => {
      this.money.set(500)
    }, 3000);
    // setTimeout(() => {
    //   this.age.xxx(18) 不能改 age，没有set方法可以调用
    // }, 3000);
  }
}
```
34. `Binding dynamic text, properties and attributes` 绑定动态的文本、组件属性和元素属性 `https://angular.dev/guide/templates/binding#binding-dynamic-properties-and-attributes`      
```text
  In Angular, a binding creates a dynamic connection between a component's template and its data. This connection ensures that changes to the component's data automatically update the rendered template.
    在Angular，一个绑定 创建了 在一个组件模板和它的数据间的 一个动态连接。这个连接，确保组件数据的修改会自动更新到已渲染的模板中。  
    ① Render dynamic text with text interpolation 使用文本插值，渲染动态的文本
    ```typescript
    @Component({
      template: `
        <p>Your color preference is {{ theme }}.</p>
      `,
      ...
    })
    export class AppComponent {
      theme = 'dark';
    }
    ```
    You can bind dynamic text in templates with double curly braces 你可以在模板使用双花括号绑定动态文本  
    双花括号里面的是 表达式 expression  
    In addition to evaluating the expression at first render, Angular also updates the rendered content when the expression's value changes.  除了第一次渲染计算表达式，当表达式的值修改了，Angular 也会更新已经渲染的内容  
    All expression values are converted to a string. Objects and arrays are converted using the value’s toString method. 所有表达式值都被转换为一个字符串。对象和数组会使用 toString 方法。  
    ② Binding dynamic properties and attributes 把动态的组件属性和元素属性绑定起来  
    Angular supports binding dynamic values into object properties and HTML attributes with square brackets. Angular 支持绑定动态值到对象属性和HTML属性，使用方括号。  
    *Native element properties 原生元素属性*  
    HTML中一个元素，会被创建要给实例，例如`<button>`会被创建一个`HTMLButtonElement`实例 `an instance of HTMLButtonElement `  
    ```html
    <!-- Bind the `disabled` property on the button element's DOM object -->
    <button [disabled]="isFormValid">Save</button>
    ```
    *Component and directive properties 组件和指令属性*  
    When an element is an Angular component, you can use property bindings to set component input properties using the same square bracket syntax.  
    当一个元素是一个Angular组件，你可以使用属性绑定设置组件input属性，使用相同的方括号语法
    ```html
    <!-- Bind the `value` property on the `MyListbox` component instance. -->
    <my-listbox [value]="mySelection" />
    ```
    In this example, every time mySelection changes, Angular automatically sets the value property of the MyListbox instance.  
    在这个例子中，每一次 mySelection修改，Angular会自动地设置 MyListbox 实例 的 value 属性  
    You can bind to directive properties as well.  
    你也可以绑定指令属性  
    ```html
    <!-- Bind to the `ngSrc` property of the `NgOptimizedImage` directive  -->
    <img [ngSrc]="profilePhotoUrl" alt="The current user's profile photo">
    ```
    更通用的方式 
    ```html
    <!-- Bind the `role` attribute on the `<ul>` element to the component's `listRole` property. -->
    <ul [attr.role]="listRole">
    ```
    In this example, every time listRole changes, Angular automatically sets the role attribute of the <ul> element by calling setAttribute.  
    在这个例子，每次 listRole 修改，Angular 自动设置role 属性，通过调用 setAttribute  
    If the value of an attribute binding is null, Angular removes the attribute by calling removeAttribute.  
    如果一个数下绑定是 null，angular 调用 removeAttribute 来移除属性  
    *Text interpolation in properties and attributes 在属性里面进行文本插值*  
    ```html
    <!-- Binds a value to the `alt` property of the image element's DOM object. -->
    <img src="profile-photo.jpg" alt="Profile photo of {{ firstName }}" >
    ```
    To bind to an attribute with the text interpolation syntax, prefix the attribute name with attr.
    ```html
    <button attr.aria-label="Save changes to {{ objectType }}">
    ```
    *CSS class and style property bindings CSS 类和样式属性绑定*  
    ```html
    <!-- When `isExpanded` is truthy, add the `expanded` CSS class. -->
    <ul [class.expanded]="isExpanded">
    ```
    ```typescript
    @Component({
      template: `
        <ul [class]="listClasses"> ... </ul>
        <section [class]="sectionClasses"> ... </section>
        <button [class]="buttonClasses"> ... </button>
      `,
      ...
    })
    export class UserProfile {
      listClasses = 'full-width outlined';
      sectionClasses = ['expandable', 'elevated'];
      buttonClasses = {
        highlighted: true,
        embiggened: false,
      };
    }
    ```
    ```html
    <ul class="full-width outlined"> ... </ul>
    <section class="expandable elevated"> ... </section>
    <button class="highlighted"> ... </button>
    ```
    When using static CSS classes, directly binding class, and binding specific classes, Angular intelligently combines all of the classes in the rendered result.  
    当使用静态地CSS类，直接地绑定类和绑定特定的类，Angular 会智能地把所有类整合在一起
    ```typescript
    @Component({
      template: `<ul class="list" [class]="listType" [class.expanded]="isExpanded"> ...`,
      ...
    })
    export class Listbox {
      listType = 'box';
      isExpanded = true;
    }
    ```
    ```html
    <ul class="list box expanded">
    ```
    Angular does not guarantee any specific order of CSS classes on rendered elements.  
    不确保class的顺序  
    If an element has multiple bindings for the same CSS class, Angular resolves collisions by following its style precedence order.  
    有冲突时的处理逻辑  
    *CSS style properties CSS样式属性*  
    ```html
    <!-- Set the CSS `display` property based on the `isExpanded` property. -->
    <section [style.display]="isExpanded ? 'block' : 'none'">
    ```
    You can further specify units for CSS properties that accept units.  
    还可设置单位
    ```html
    <!-- Set the CSS `height` property to a pixel value based on the `sectionHeightInPixels` property. -->
    <section [style.height.px]="sectionHeightInPixels">
    ```
    ```typescirpt
    @Component({
      template: `
        <ul [style]="listStyles"> ... </ul>
        <section [style]="sectionStyles"> ... </section>
      `,
      ...
    })
    export class UserProfile {
      listStyles = 'display: flex; padding: 8px';
      sectionStyles = {
        border: '1px solid black',
        'font-weight': 'bold',
      };
    }
    ```
    ```html
    <ul style="display: flex; padding: 8px"> ... </ul>
    <section style="border: 1px solid black; font-weight: bold"> ... </section>
    ```
    When binding style to an object, Angular compares the previous value to the current value with the triple-equals operator (===). You must create a new object instance when you modify these values in order to Angular to apply any updates.  
    修改样式，要创建新的对象实例才能生效？
    If an element has multiple bindings for the same style property, Angular resolves collisions by following its style precedence order.  
    冲突的处理逻辑
```
35. `CommonModule` 通用模块，Exports all the basic Angular directives and pipes, such as NgIf, NgForOf, DecimalPipe, and so on. 导出所有基础的Angular指令和管道，例如 NgIf NgForOf DecimalPipe 
36. `*ngFor` `*ngIf` ... 是语法糖，是简写形式，推荐使用简写形式，`https://angular.dev/guide/directives/structural-directives#shorthand-examples`  
    `*ngFor="let item of [1,2,3]"	` 会被解释(interpret)成 `<ng-template ngFor let-item [ngForOf]="[1, 2, 3]">`  
    `*ngIf="exp"` 会被解释(interpret)成
    `<ng-template [ngIf]="exp">`  
    例如
    ```html
        <ul>
          <li *ngFor="let name of names">{{name}}</li>
        </ul>
        <ul>
          <ng-template ngFor let-name [ngForOf]="names">
            <li>{{name}}</li>
          </ng-template>
        </ul>
    ```
37. The constructor is the first function that runs when this component is created. 构造器 是 当 这个组件被创建时 运行的第一个函数。
38. 依赖注入方式  
ng generate service log
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LogService {
  constructor() { }
  info(msg: string) {
    console.log(msg);
  }  
  warn(msg: string) {
    console.warn(msg);
  }
}
```
```typescript
@Component({ /* ... */ })
export class HomeComponent {
  logService: LogService = inject(LogService)
  constructor() {
    this.logService.info("哈哈")
    this.logService.warn("嘻嘻")
  }
}
```
```typescript
@Component({ /* ... */ })
export class HomeComponent {
  logService: LogService
  constructor() {
    this.logService = inject(LogService)
    this.logService.info("哈哈2")
    this.logService.warn("嘻嘻2")
  }
}
```
```typescript
@Component({ /* ... */ })
export class HomeComponent {
  constructor(logService: LogService) {
    logService.info("哈哈3")
    logService.warn("嘻嘻3")
  }
}
```
39. Routing helps you change what the user sees in a single-page app. 路由可帮助您改变用户在单页应用程序中看到的内容。
40. `ng generate component first` CLI 会自动追加Component，因此，如果您要写入first-component，则您的组件将是FirstComponentComponent。
41. 默认路由匹配的空路径路由。路线顺序，路由的顺序很重要，因为Router在匹配路由时使用先匹配获胜策略，因此更具体的路由应置于不太具体的路由之上。首先列出具有静态路径的路由，然后列出与默认路由匹配的空路径路由。通配符路由排在最后，因为它与每个 URL 匹配，并且Router只有在没有其他路由首先匹配时才会选择它。
42. `{ path: '**', component: <component-name> }` 两个星号`**`向 Angular 表明此routes定义是通配符路由。对于 component 属性，您可以定义应用程序中的任何组件。常见的选择包括特定于应用程序的PageNotFoundComponent，您可以将其定义为向用户显示 404 页面；或重定向到应用程序的主要组件。通配符路由是最后一条路由，因为它匹配任何 URL。
```typescript
const routes: Routes = [
  { path: 'first-component', component: FirstComponent },
  { path: 'second-component', component: SecondComponent },
  { path: '**', component: PageNotFoundComponent },  // Wildcard route for a 404 page
];
```
43. 路由重定向 redirectTo。页面标题，还可动态设置。
44. 路由嵌套、子路由 `https://angular.dev/guide/routing/common-router-tasks#nesting-routes`
```typescript
const routes: Routes = [
  {
    path: 'first-component',
    component: FirstComponent, // this is the component with the <router-outlet> in the template
    children: [
      {
        path: 'child-a', // child route path
        component: ChildAComponent, // child route component that the router renders
      },
      {
        path: 'child-b',
        component: ChildBComponent, // another child route component that the router renders
      },
    ],
  },
];
```
45. 相对路由。除 `../` 之外，使用 `./` 或不使用前导斜杠来指定当前级别。
```typescript
<h2>First Component</h2>
<nav>
  <ul>
    <li><a routerLink="../second-component">Relative Route to second component</a></li>
  </ul>
</nav>
<router-outlet></router-outlet>
```
46. 延迟加载。
```typescript
const routes: Routes = [
  {
    path: 'lazy',
    loadComponent: () => import('./lazy.component').then(c => c.LazyComponent)
  }
];
```
47. 防止未经授权的访问。使用路由守卫来防止用户未经授权导航到应用程序的某些部分。要使用路由保护，请考虑使用无组件路由，因为这有助于保护子路由。
48. `https://angular.dev/guide/routing/common-router-tasks#link-parameters-array`
49. Angular 单页应用 SPA 不用重复加载页面。
```
PS C:\Users\zhouhuajian\Desktop\first-app> npx serve .\dist\first-app\browser\

   ┌──────────────────────────────────────────┐
   │                                          │
   │   Serving!                               │
   │                                          │
   │   - Local:    http://localhost:3000      │
   │   - Network:  http://192.168.30.1:3000   │
   │                                          │
   │   Copied local address to clipboard!     │
   │                                          │
   └──────────────────────────────────────────┘

 HTTP  02/01/2025 12:23:12 ::1 GET /  （页面只加载了一次）
 HTTP  02/01/2025 12:23:12 ::1 Returned 200 in 27 ms
 HTTP  02/01/2025 12:23:13 ::1 GET /polyfills-FFHMD2TL.js
 HTTP  02/01/2025 12:23:13 ::1 GET /main-H6M6M7UM.js
 HTTP  02/01/2025 12:23:13 ::1 GET /styles-GSBFIRKP.css
 HTTP  02/01/2025 12:23:13 ::1 Returned 200 in 13 ms
 HTTP  02/01/2025 12:23:13 ::1 Returned 200 in 10 ms
 HTTP  02/01/2025 12:23:13 ::1 Returned 200 in 15 ms
 HTTP  02/01/2025 12:23:13 ::1 GET /assets/logo.svg
 HTTP  02/01/2025 12:23:13 ::1 Returned 200 in 21 ms
 HTTP  02/01/2025 12:23:13 ::1 GET /assets/location-pin.svg
 HTTP  02/01/2025 12:23:13 ::1 Returned 200 in 20 ms
 HTTP  02/01/2025 12:23:15 ::1 GET /favicon.ico
 HTTP  02/01/2025 12:23:15 ::1 Returned 200 in 38 ms
 HTTP  02/01/2025 12:23:37 ::1 GET /favicon.ico
 HTTP  02/01/2025 12:23:37 ::1 Returned 304 in 2 ms
 HTTP  02/01/2025 12:24:10 ::1 GET /favicon.ico
 HTTP  02/01/2025 12:24:10 ::1 Returned 304 in 6 ms
 HTTP  02/01/2025 12:24:10 ::1 GET /assets/location-pin.svg
 HTTP  02/01/2025 12:24:10 ::1 Returned 304 in 3 ms
 HTTP  02/01/2025 12:24:19 ::1 GET /favicon.ico
 HTTP  02/01/2025 12:24:19 ::1 Returned 304 in 1 ms
 HTTP  02/01/2025 12:24:29 ::1 GET /favicon.ico
 HTTP  02/01/2025 12:24:29 ::1 Returned 304 in 2 ms
```
50. Link parameters array （可以直接写href即可，但这种方式，可以更加灵活地生成 href，多少层的路由都可以支持，其实可以理解为是 href 的 builder）链接参数数组 `https://angular.dev/guide/routing/common-router-tasks#link-parameters-array`  
链接参数数组包含路由器导航的以下要素：  
到目标组件的路由路径  
路由 URL 中的必需和可选路由参数
In summary, you can write applications with one, two or more levels of routing. The link parameters array affords the flexibility to represent any routing depth and any legal sequence of route paths, (required) router parameters, and (optional) route parameter objects.  
```html
Navigate to <a routerLink="/@Angular">my profile</a>

<a [routerLink]="['/heroes']">Heroes</a>
<a [routerLink]="['/hero', hero.id]">
  <span class="badge">{{ hero.id }}</span>{{ hero.name }}
</a>
<a [routerLink]="['/crisis-center', { foo: 'foo' }]">Crisis Center</a>
<a [routerLink]="['/crisis-center']">Crisis Center</a>
<a [routerLink]="['/crisis-center', 1]">Dragon Crisis</a>
<a [routerLink]="['/crisis-center']">Crisis Center</a>
<a [routerLink]="['/crisis-center/1', { foo: 'foo' }]">Dragon Crisis</a>
<a [routerLink]="['/crisis-center/2']">Shark Crisis</a>
```
51.  (required) router parameters, and (optional) route parameter objects. `http://localhost:4200/post/1;op1=1;op2=2?rp=1&rp=2`
```typescript
@Component({
 /* ... */
})
export class PostComponent {
  postId = -1;
  constructor(private route: ActivatedRoute, private router: Router) {
    // 使用代码跳转页面
    // this.router.navigate(['/'], { queryParams: { 'page': 1 } })

    // 必填路由参数
    this.postId = Number(this.route.snapshot.params['id']);
    console.log(this.route.snapshot.params, this.postId);

    // 可选路由参数 用 paramMap和params都能获得
    const op1 = this.route.snapshot.paramMap.get('op1');
    const op2 = this.route.snapshot.paramMap.get('op2');
    console.log(this.route.snapshot.paramMap, op1, op2);

    // 查询参数
    const rp1 = this.route.snapshot.queryParams['rp1'];
    const rp2 = this.route.snapshot.queryParams['rp2'];
    console.log(this.route.snapshot.queryParams, rp1, rp2)
  }
}
```
52. LocationStrategy和浏览器 URL 样式。现代 HTML5 浏览器支持history.pushState，这是一种无需触发服务器页面请求即可更改浏览器位置和历史记录的技术。路由器可以编写一个“自然”的 URL，该 URL 与原本需要页面加载的 URL 难以区分。可以改成 `#` 风格的 URL。该RouterModule.forRoot()函数将 设置LocationStrategy为PathLocationStrategy，使其成为默认策略。您还可以选择HashLocationStrategy在引导过程中使用覆盖切换到 。
53. `<base href>` `您必须向应用程序添加一个<base href>元素index.html才能使pushState路由正常工作。浏览器<base href>在引用 CSS 文件、脚本和图像时使用该值作为相对 URL 的前缀。`
54. 组件模板里面的注释`<!-- -->`不会输出到页面。Comments in the template source code are not included in the rendered output `https://angular.dev/guide/templates#differences-from-standard-html`
55. 单页应用，默认情况下，普通的web服务器，不能一开始就访问其他页面，例如不能一开始就访问 `http://localhost:3000/post/1;op1=1;op2=2?rp1=1&rp2=2`，会404，当然这个应该可以通过，web服务器的重定向来解决这个问题。
```text
PS C:\Users\zhouhuajian\Desktop\first-app> npx serve .\dist\first-app\browser\
 WARN  Checking for updates failed (use `--debug` to see full error)

   ┌──────────────────────────────────────────┐
   │                                          │
   │   Serving!                               │
   │                                          │
   │   - Local:    http://localhost:3000      │
   │   - Network:  http://192.168.30.1:3000   │
   │                                          │
   │   Copied local address to clipboard!     │
   │                                          │
   └──────────────────────────────────────────┘

 HTTP  02/01/2025 18:23:43 ::1 GET /post/1;op1=1;op2=2?rp1=1&rp2=2
 HTTP  02/01/2025 18:23:43 ::1 Returned 404 in 33 ms
 HTTP  02/01/2025 18:23:44 ::1 GET /favicon.ico
 HTTP  02/01/2025 18:23:44 ::1 Returned 304 in 8 ms
```
56. The Angular Router is an optional service that presents a particular component view for a given URL. It isn't part of the Angular core and thus is in its own library package, @angular/router.  
Import what you need from it as you would from any other Angular package.
Router 是一个可选的服务 service。
57. A routed Angular application has one singleton instance of the Router service.  When the browser's URL changes, that router looks for a corresponding Route from which it can determine the component to display.A router has no routes until you configure it.  
58. Each Route maps a URL path to a component. There are no leading slashes in the path. The router parses and builds the final URL for you, which lets you use both relative and absolute paths when navigating between application views.   
59. Router outlet  
The RouterOutlet is a directive from the router library that is used like a component. It acts as a placeholder that marks the spot in the template where the router should display the components for that outlet.
```html
<router-outlet></router-outlet>
<!-- Routed components go here -->
```
Given the preceding configuration, when the browser URL for this application becomes /heroes, the router matches that URL to the route path /heroes and displays the HeroListComponent as a sibling element to the RouterOutlet that you've placed in the host component's template.    
60. Had the navigation path been more dynamic, you could have bound to a template expression that returned an array of route link parameters; that is, the link parameters array. The router resolves that array into a complete URL.  
61. Active router links  
The RouterLinkActive directive toggles CSS classes for active RouterLink bindings based on the current RouterState.  
On each anchor tag, you see a property binding to the RouterLinkActive directive that looks like  
```html
routerLinkActive="..."
```
The template expression to the right of the equal sign, =, contains a space-delimited string of CSS classes that the Router adds when this link is active and removes when the link is inactive. You set the RouterLinkActive directive to a string of classes such as routerLinkActive="active fluffy" or bind it to a component property that returns such a string. For example,
```html
[routerLinkActive]="someStringProperty"
```
Active route links cascade down through each level of the route tree, so parent and child router links can be active at the same time. To override this behavior, bind to the `[routerLinkActiveOptions]` input binding with the { exact: true } expression. By using { exact: true }, a given RouterLink is only active if its URL is an exact match to the current URL.  
62. `provideRouter` provides the necessary service providers for navigating through application views.  
63. `RouterLink`	The directive for binding a clickable HTML element to a route. Clicking an element with a routerLink directive that's bound to a string or a link parameters array triggers a navigation.  
64. `ActivatedRoute`	A service that's provided to each route component that contains route specific information such as route parameters, static data, resolve data, global query parameters, and the global fragment.  
65. `Routing component`	An Angular component with a RouterOutlet that displays views based on router navigations.   
66. Router state  
After the end of each successful navigation lifecycle, the router builds a tree of ActivatedRoute objects that make up the current state of the router. You can access the current RouterState from anywhere in the application using the Router service and the routerState property.  
Each ActivatedRoute in the RouterState provides methods to traverse up and down the route tree to get information from parent, child, and sibling routes.  
67. The routerLink directive enables Angular's router to create dynamic links in the application.   
68. This code gives the DetailsComponent access to the ActivatedRoute router feature that enables you to have access to the data about the current route.   
69. Notice that the housingLocation properties are being accessed with the optional chaining operator ?. This ensures that if the housingLocation value is null or undefined the application doesn't crash.  
70. 这个 ipt 就是表示 `<input>` 元素，跟 `document.querySelector()` 拿到的一样
```html
      <form>
        <input type="text" placeholder="Filter by city" #ipt />
        <button class="primary" type="button" (click)="filterResults(ipt.value)">Search</button>
      </form>
```
71. Angular has two types of variable declarations in templates: local template variables and template reference variables.
局部模板变量和模板引用变量
@let和 JavaScript 的一个关键区别let是，@let声明后不能重新赋值。但是，Angular 会自动根据给定的表达式更新变量的值。
```html
@let value = 1;
<!-- Invalid - This does not work! -->
<button (click)="value = value + 1">Increment the value</button>
```
模板引用变量可以引用以下内容： 
```text
模板内的 DOM 元素（包括自定义元素）  
Angular 组件或指令  
来自ng-template的TemplateRef
```
```html
<!-- Create a template reference variable named "taskInput", referring to the HTMLInputElement. -->
<input #taskInput placeholder="Enter task name">
```
如果在 Angular 组件上声明变量，则该变量指的是组件实例。
```html
<!-- The `startDate` variable is assigned the instance of `MyDatepicker`. -->
<my-datepicker #startDate />
```
如果您在元素上声明变量<ng-template>，则该变量引用代表模板的 TemplateRef 实例。
```html
<!-- The `myFragment` variable is assigned the `TemplateRef` instance corresponding to this template fragment. -->
<ng-template #myFragment>
  <p>This is a template fragment</p>
</ng-template>
```
如果在任何其他显示元素上声明变量，则该变量引用该HTMLElement实例。
```html
<!-- The "taskInput" variable refers to the HTMLInputElement instance. -->
<input #taskInput placeholder="Enter task name">
```
72. @ViewChild
```
作用：
获取组件或指令实例：通过 @ViewChild 你可以很方便地获取模板中子组件的实例，从而调用这个子组件的方法或是访问它的属性。
操作 DOM 元素：有时你需要直接操作 DOM 元素，例如设置焦点或更改样式。通过 @ViewChild，你可以在代码中直接引用到模板中的元素。
访问模板引用变量：在模板中定义的引用变量（通过 # 语法），可以通过 @ViewChild 在组件类中获取，从而进行更复杂的操作和逻辑处理。
```
```text
export interface ViewChildDecorator {
  /**
   * @description
   * Property decorator that configures a view query.
   * The change detector looks for the first element or the directive matching the selector
   * in the view DOM. If the view DOM changes, and a new child matches the selector,
   * the property is updated.
```
73. （未验证，来自网络）Angular一共提供了19中内置的装饰器，其中有5个类装饰器、6个属性装饰器、2个方法装饰器和6个参数装饰器。
74. HttpClient  
默认情况下，HttpClient使用XMLHttpRequestAPI 发出请求。此withFetch功能可让客户端改为使用fetchAPI。fetch是一种更现代的 API，可用于一些XMLHttpRequest不支持的环境。但它也有一些限制，例如不产生上传进度事件。  
```typescript
export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(
      withFetch(),
    ),
  ]
};
```
withJsonpSupport()  
包括withJsonpSupport启用.jsonp()的方法，该方法通过JSONP 约定HttpClient发出 GET 请求，用于跨域加载数据。
有帮助：如果可能的话，最好使用CORS而不是 JSONP 进行跨域请求。  
进度事件默认是禁用的（因为它们会影响性能），但可以通过reportProgress选项启用。  
注意：fetch的可选实现HttpClient不报告上传进度事件。  
HTTP 请求失败的原因有两种：  
网络或连接错误可能会阻止请求到达后端服务器。  
后端可以接收请求但无法处理，并返回错误响应。  
有时，网络中断等瞬态错误可能会导致请求意外失败，只需重试请求即可使其成功。RxJS 提供了几个重试运算符，可在特定条件下自动重新订阅失败的请求Observable。例如，retry()运算符将自动尝试重新订阅指定的次数。  
HttpClient产生 RxJS 所称的“冷” Observable，这意味着在Observable订阅之前不会发生任何实际请求。只有这样，请求才会真正发送到服务器。Observable多次订阅同一个 会触发多个后端请求。每个订阅都是独立的。  
订阅后，取消订阅将中止正在进行的请求。如果Observable通过async管道订阅了，这将非常有用，因为如果用户离开当前页面，它将自动取消请求。此外，如果您将Observable与 RxJS 组合器（如）一起使用switchMap，则此取消将清除所有过时的请求。  
一旦响应返回，ObservablesHttpClient通常就完成了（尽管拦截器可以影响这一点）。    
由于自动完成，如果不清理订阅，通常不会有内存泄漏的风险HttpClient。但是，与任何异步操作一样，我们强烈建议您在使用订阅的组件被销毁时清理订阅，否则订阅回调可能会运行并在尝试与被销毁的组件交互时遇到错误。  
提示：使用async管道或toSignal操作订阅Observables 可确保正确处理订阅  
75. HttpClient 最佳实践  https://angular.dev/guide/http/making-requests#best-practices  
虽然HttpClient可以直接从组件注入和使用，但通常我们建议您创建可重复使用的可注入服务，以隔离和封装数据访问逻辑。例如，这UserService封装了通过用户 ID 请求用户数据的逻辑：  
```typescript
@Injectable({providedIn: 'root'})
export class UserService {
  constructor(private http: HttpClient) {}
  getUser(id: string): Observable<User> {
    return this.http.get<User>(`/api/user/${id}`);
  }
}
```
在组件内，您可以结合@if管道async，仅在数据加载完成后才呈现数据 UI：
```typescript
import { AsyncPipe } from '@angular/common';
@Component({
  imports: [AsyncPipe],
  template: `
    @if (user$ | async; as user) {
      <p>Name: {{ user.name }}</p>
      <p>Biography: {{ user.biography }}</p>
    }
  `,
})
export class UserProfileComponent {
  @Input() userId!: string;
  user$!: Observable<User>;
  constructor(private userService: UserService) {}
  ngOnInit(): void {
    this.user$ = this.userService.getUser(this.userId);
  }
}
```
76. 使用 ng-content 插入子内容 Slotting child content with ng-content `https://angular.dev/guide/templates/ng-content`
77. 使用 ng-template 创建模板片段 Create template fragments with ng-template `https://angular.dev/guide/templates/ng-template`
78. 使用 ng-container 对元素进行分组 Grouping elements with ng-container `https://angular.dev/guide/templates/ng-container`





todo: @Injectable、service provider 、router、Observable the router builds a tree of ActivatedRoute objects that make up the current state of the router.
