# angular-manual

https://angular.dev/  
https://github.com/angular/angular

HTML标签尖括号 `<>` 叫做 `Angular Brackets` 或者 `Angle Brackets`，这是 `Angular` 名字的由来，为了扩展 HTML。

指令 directives 可以扩展 HTML 标签和 HTML 属性。

Directives are classes that add additional behavior to elements in your Angular applications. 

指令是一些类，这些类在你的应用程序中 给 元素 添加额外的行为。

`@angular/core` `@angular/common` ... 这些都是一些 `Angular` npm 包，不同的包里面，会把不同的功能聚在一起。

模块 Module 把 一些组件、指令、管道 整合在一起。可以把庞大的功能分成一个一个划分清晰的模块，例如按业务不同，划分模块。

CSS 扩展语言

`GetAngular` -> `AngularJS` -> `Angular`

`filter` -> `pipe` 

组件、表单、路由、依赖注入、信号、延迟加载、Angular CLI、Angular DevTools、内置变量

双花括号`{{}}`——元素内容、元素属性值 文本插值（语法）、方括号`[]`——元素属性、圆括号`()`——元素事件、"banana-in-a-box"`[()]`——双向绑定 Two-way binding、指令`*`directive

三个 Structural directives，v17之前`*ngFf`、`*ngFor`、`*ngSwitch`，v17之后可以使用`@if`、`@else`、`@for`、`@switch`进行替代，更直观，代码可读性更好

https://angularjs.org/ 这个网站不再维护，AngularJS 项目已被 Google 关闭，不再维护，老项目 AngularJS 已被 Google 新项目 Angular 替代   
https://angular.io/ 这个网站不再更新，大部分页面会自动跳转到 https://angular.dev/

In Angular, the `ng` stands for `Angular`. 

`<app-root></app-root>` 这种元素，就是一个Angular组件（实例）。`When an element is an Angular component, ...`

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
35. `CommonModule` 通用模块，Exports all the basic Angular directives and pipes, such as NgIf, NgForOf, DecimalPipe, and so on. 导出所有基础的Angular指令和管道，例如 NgIf NgForOf DecimalPipe 
36. `*ngFor` `*ngIf` ... 是语法糖，是简写形式，推荐使用简写形式，`https://angular.dev/guide/directives/structural-directives#shorthand-examples`  
`*ngFor="let item of [1,2,3]"	` 会被解释(interpret)成 `<ng-template ngFor let-item [ngForOf]="[1, 2, 3]">`  
`*ngIf="exp"` 会被解释(interpret)成 `<ng-template [ngIf]="exp">`  
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
