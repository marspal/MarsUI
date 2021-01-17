## React UI Component

### 基础知识

- 状态提升 or 单项数据流

  通常可变的数据都有一个单一的数据流

- 配置React开发环境
  create-react-app 安装: npx create-react-app my-app --typescript
  **npx 作用**: 会将node_modules/bin加入path变量; 结束后删除
  1. 避免安装全局模块
  2. 调用内部安装模块 如: npx mocha --version

- Hook规则
  1. 只在最顶层使用Hook
  2. 只在函数中调用Hook

### 组件架构

- 目录结构和代码规范

  1. 目录结构
```
  |--.storybook storybook相关配置 
  |--node_modules
  |--public
  |--src
      |-- components
         |--Button
            |--button.tsx
            |--button.test.tsx
            |--style.scss 组件单独样式
      |-- styles 全局样式文件
        _variables.scss (各种变量以及可配置设置)
        _minxins.scss (全局mixins)
        _functions.scss (全局functions)
        index.scss (样式入口文件)
```       

  2. 代码规范
    create-react-app天生自带项目规范; .eslintrc中配置相关规则; 注意: 开启vscode编辑器 ESLint按钮

- [样式解决方案](https://reactjs.org/docs/faq-styling.html)

> 方案:
  1. inlineStyle: class性能要比instyle好很多
  2. CSS in JS: 如 style Component; React 中立态度; 不建议使用
  3. Sass/Less: 推荐

> Q: 如何创建组件库的色彩体系
  1. 创建系统色板 - 基础色板 + 中性色板 [色板](http://zhongguose.com/)
  
  ```scss
  // 中性色板; from white to black !default scss提供的, 用户定义后 不在赋值
  $white:    #fff !default;
  $gray-100: #f8f9fa !default;
  $gray-200: #e9ecef !default;
  $gray-300: #dee2e6 !default;
  $gray-400: #ced4da !default;
  $gray-500: #adb5bd !default;
  $gray-600: #6c757d !default;
  $gray-700: #495057 !default;
  $gray-800: #343a40 !default;
  $gray-900: #212529 !default;
  $black:    #000 !default;

  // 基础色板
  $blue:    #0d6efd !default;
  $indigo:  #6610f2 !default;
  $purple:  #6f42c1 !default;
  $pink:    #d63384 !default;
  $red:     #dc3545 !default;
  $orange:  #fd7e14 !default;
  $yellow:  #fadb14 !default;
  $green:   #52c41a !default;
  $teal:    #20c997 !default;
  $cyan:    #17a2b8 !default;

  // 系统色板
  $primary:       $blue !default;
  $secondary:     $gray-600 !default;

  // 功能色

  // 字体系统

  // 链接

  // 表单

  // 按钮

  // 边框和阴影

  // 可配置开关

  ```

  2. 产品色板 - primary + secondery
  ```scss
    $success:       $green !default;
    $info:          $cyan !default;
    $warning:       $yellow !default;
    $danger:        $red !default;
    $light:         $gray-100 !default;
    $dark:          $gray-800 !default;
  ```

  3. 引入normalize.css: 解决不同浏览器兼容问题

  4. 需要导出scss入口文件
  
  注意: _ 称为partials 告诉scss不要编译到css文件; 只能被导入

- 组件需求和编码

> Q: 如何开发第一个组件Button组件?

  1: 明确需求，确定Button Type、Button Size、Disabled状态; 编写JS组件
  2: 写入组件样式 按钮的大小由padding、font-size、border-radius控制; 颜色由
    border-color、background、color控制
  3: mixin解决重复代码问题
  4: 原生属性支持ButtonHTMLAttributes<HTMLElement>获取所有的btn原生属性

- 组件测试用例分析和编码

> Q: 为什么要有测试
  
  有测试对代码升级叫重构;没测试代码升级叫重写;

  作用:
  1. 高质量的代码
  2. 更早的发现bug,减少成本
  3. 让重构和升级更加容易和升级
  4. 让开发流程更加敏捷
```flow
  st=>start: Start
  op=>operation: Unit
  op=>operation: Service
  op=>operation: Service
  e=>end: End
```
  React组件类型更加合适写单元测试
  1. Component - 组件
  2. Function - 函数
  3. 单项数据流
> Q: 如何搭建组件测试架构
  
  1. Jest框架 
  2. React Testing Library
  3. jest-dom: 新增DOM断言 
对JEST matchers 进行扩展import '@testing-library/jest-dom/extend-expect';

  使用如上三个库,搭建结束项目测试框架


> Q: 如何编写测试用例



- 代码打包输出和发布

- CI/CD, 文档生成等等

> storybook 解决本地调试和文档页面生成利器

**CRA缺点:**

1. CRA 入口文件不合适管理组件库
2. 缺少行为追踪和属性

>Q: 完美的组件应具有什么特点?

1. 具有分开展示各个组件不同属性下的状态
2. 具有能追踪组件行为并具有属性调试功能
3. 具有为组件自动生成生成文档和属性列表

storybook完美解决上述问题

> storybook 安装使用

1. npm run @storybook/react

Q: storybook支持typescript

在.storybook添加相关配置;
在每一个组件中加入自己的story文件button.stories.tsx
react-docgen: 处理注释显示 显示出来

2. 安装addons 
cnpm i @storybook/addon-actions @storybook/addon-links @storybook/addon-essentials -D
### 易错知识点

1. a 标签没有disabled? 加上disabled属性模拟实现


> TS 常用的知识点

Partial<T> : 属性可选