![node-playbook banner](http://i.imgur.com/C1yh7Wj.png)

# Node.js 指南

这是一篇有主见的Node.js新手开发指南。

(原文地址：https://github.com/cuitianze/no-fullstack-no-fe/blob/master/1-Node.js入门指南.md)

### 为何而生
你总是浪费时间在:

* 发现/研究Node.js最基础的方面, 在实现相同工作的几个工具中纠结地选择。

### 学习推荐
追随指南. 它推荐了最基本的选择，让你专注在编程上，而不是在配置上。

### 为谁而生

* 那些想动手做一个项目，但不想碰到太多麻烦的新手
* 那些想快速上手，但是不太熟悉Node.js生态的老兵

### 此非何物

* 不会教你JavaScript
* 这不是开发Node.js的 **唯一方式**. 通过此指南入门，然后选择其他更适合的方案
* 这不是开发Node.js的 **最好方式**. 这是一个足以避免很多学习天花板的入门指南
* 这不会替代你阅读官方文档的需求
* 不是所有的建议都为Node.js量身打造

### 如何选择解决方案？

解决方案的选择需要先权衡以下几点:

* 是否成熟? (看看有没有发布版本1)
* 是否被积极地维护?
* 是否有一个好的文档?
* 是否流行? (因而你可以找到大量的教程和支持的社区)
* 是否免费开源? (尽可能，除了服务器托管和域名)
* 是否易学?
* 是否适合日常实际开发?
* 是否和指南里提到的其他方案完美配合?

## 目录

1. [金科玉律: 尽可能少写代码](#金科玉律: 尽可能少写代码)
1. [常见问题](#general-problems)
  1. [Node.js 版本](#nodejs-version)
  1. [开发环境](#development-environment)
  1. [工作流](#workflow)
  1. [文件与文件夹结构](#file-and-folder-structure)
  1. [编码风格](#coding-style)
  1. [原生模块和Windows系统](#native-modules-and-windows)
1. [web开发](#developing-for-the-web)
  1. [技术栈](#technology-stack)
1. [开发一个包](#developing-a-package)
  1. [版本号](#version-numbering)
1. [开发移动应用](#developing-mobile-applications)
1. [开发桌面应用](#developing-desktop-applications)
  1. [跨平台框架](#cross-platform-framework)
1. [即将更新](#upcoming-sections)
1. [贡献](#contributing)
1. [License](#license)

# 金科玉律: 尽可能少写代码
最佳的偷懒，只有两个原则:

1. 完成一个任务的最快方式就是什么也不做
  * 问问你自己，如果没有它是否还能运行应用
  * 越少的代码意味着越少的bug
  * 相关推荐:
    * [You aren't gonna need it](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it) (YAGNI)
    * [Customer development](http://www.startuplessonslearned.com/2008/11/what-is-customer-development.html)
    * [Minimum viable product](http://www.startuplessonslearned.com/2009/08/minimum-viable-product-guide.html) (MVP)
1. 完成一个任务的第二快方式是站在巨人的肩膀上
  * 举个例子, 本指南就是众人的工作总结
  * 使用 [Node.js 核心 API](https://nodejs.org/api/) 
  * 使用已有的代码段, 比如 [npm packages](https://www.npmjs.com/)
    * 确保你使用的都是高质量的依赖

# General problems
This section covers general problems regardless of your development goals.

## Node.js version
### Problem / Context
Many versions are listed on the Node.js website. Choosing a Node.js version wastes time.
### Recommended solution
Choose [Node.js v6](https://nodejs.org/dist/latest-v6.x/). It will enter long term support (LTS) on October 1, 2016, after which it will stay in LTS for 18 months. This gives you peace of mind against major new features popping up in Node.js while you build your app.

## Development environment
### Problem / Context
Choosing a development environment (e.g. editors, git GUIs, terminals, FTP clients) wastes time. No tool is 10 times better than another. You need a set of tools that get you started and let you grow according to you needs.
### Recommended solution
Download and install these tools:
* Editor: [Atom](https://atom.io/)
  * Atom packages/plug-ins:
    * atom-beautify (go into `Settings > Packages` and enable `Beautify On Save` for CSS, HTML, JavaScript, JSON, and Markdown)
    * atom-html-preview (press `Ctrl+P` in the editor to open the preview)
    * fold-lines
    * terminal-plus
    * markdown-preview (press `Ctrl+Shift+M` in the editor to open the preview)
* Version control: [git](https://git-scm.com/)
* Repository (repo) hosting: [GitHub](https://github.com/)
  * for private repos: either pay GitHub or use [BitBucket](https://bitbucket.org/) instead
* Git GUI: [SourceTree](https://www.sourcetreeapp.com/) (why: you can upload/push much faster and clone repos from GitHub *and* BitBucket)
* API testing: [Postman](https://www.getpostman.com/apps)
* Socket testing: [Socket.io tester](https://chrome.google.com/webstore/detail/socketio-tester/cgmimdpepcncnjgclhnhghdooepibakm?hl=en)

## Workflow
### Problem / Context
Thinking about how to set up a new project wastes time.
### Recommended solution
1. Create a new repo on either GitHub or BitBucket
  * Choose Node under the gitignore settings when creating a repo
  * Choose to create a README.md
1. Clone it to your computer with either a terminal command or with SourceTree
1. Set up your [file and folder structure](#file-and-folder-structure)
1. Open a terminal window in your repo folder (or use the Terminal button when you open the repo in SourceTree)
1. Run `npm init` in your terminal to create a `package.json` file
  * Set your initial version to 0.1.0 (see also [version numbering](#version-numbering))
  * If this is an open source project then choose an MIT license by typing `MIT` when prompted for a license name
1. Run `atom ./` in your terminal to launch Atom in your project folder

## File and folder structure
### Problem / Context
Thinking about how to set up your project file and folder structure wastes time.
### Recommended solution
1. Create three subfolders:
  1. `source`: place all your source code here
  1. `test`: place all testing code here
  1. `build` (optional): use this as a destination folder if/when you implement a build system (something that converts your source code to another form)
1. Create a file in the `source` sub-folder called `index.js`

## Coding style
### Problem / Context
Fretting over coding style wastes time, and a sloppy coding style reflects poorly on you. You need a coding style that looks decent and is easy to follow.
### Recommended solution
Follow [Airbnb's Javascript Style Guide](https://github.com/airbnb/javascript)

## Native modules and Windows
### Problem / Context
Some npm packages do not install on Windows because they contain non-JavaScript code. You will see errors related to `node-gyp` when you try to install them.
### Recommended solution
Find another npm package that does the job in pure JavaScript. For example, [bcryptjs](https://www.npmjs.com/package/bcryptjs) is a drop-in replacement for the popular [bcrypt](https://www.npmjs.com/package/bcrypt) module.

How to find alternatives:
* if the repo is hosted on GitHub or a similar platform, search the Issues for anyone mentioning Windows or node-gyp. It is likely someone in the thread has linked to a pure JavaScript replacement
* search online

Make sure that your chosen alternative is a suitable replacement. Look for:
* recently active contributors
* good documentation
* number of downloads

This is the simplest solution as it eliminates the problem rather than trying to accommodate it. The speed advantage from the native module will not be missed until later in your development cycle.
### Alternative solution
Do this **if and only if** you cannot find a suitable alternative npm package.

Follow the Windows installation instructions at the [node-gyp README](https://github.com/nodejs/node-gyp#Installation).

I never got this to work despite many tries.

# Developing for the web
This section covers problems commonly encountered with developing, deploying, and distributing web applications.

## Technology stack
### Problem / Context
Choosing a technology stack (e.g. server framework, database, front-end framework, hosting platform) wastes time. Every stack is different and affects your project, however this is mostly a matter of style. Every stack will do the job.
### Recommended solution
* Back-end:
  * Hosting: [Heroku](https://www.heroku.com/)
  * Server framework: [express](https://www.npmjs.com/package/express)
  * Database: PostgresSQL (host it on Heroku)
  * Object-relational mapping: [Sequelize](https://www.npmjs.com/package/sequelize)
* Front-end
  * Domain: [Namecheap](https://www.namecheap.com/domains/registration.aspx?aff=103766) (affiliate link) [[non-affiliate link](https://www.namecheap.com/domains/registration.aspx)]
  * Hosting: [Namecheap](https://www.namecheap.com/hosting/shared.aspx?aff=103766) (affiliate link) [[non-affiliate link](https://www.namecheap.com/hosting/shared.aspx)] (looking for free CDN suggestions that support custom domains)
  * JavaScript: no recommendation yet
  * Styling: [Bootstrap](http://getbootstrap.com/)

# Developing a package
This section covers problems commonly encountered with developing and publishing reusable packages.

## Version numbering
### Problem / Context
Deciding on a version number scheme wastes time. Using a non-standard scheme confuses anyone using your package.
### Recommended solution
Use [Semantic Versioning](http://semver.org/) (a.k.a. semver). Here are the most important bits to get started:

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> 1. MAJOR version when you make incompatible API changes,
> 2. MINOR version when you add functionality in a backwards-compatible manner, and
> 3. PATCH version when you make backwards-compatible bug fixes.
>
> How should I deal with revisions in the 0.y.z initial development phase?
>
> The simplest thing to do is start your initial development release at 0.1.0 and then increment the minor version for each subsequent release.
>
> How do I know when to release 1.0.0?
>
> If your software is being used in production, it should probably already be 1.0.0. If you have a stable API on which users have come to depend, you should be 1.0.0. If you’re worrying a lot about backwards compatibility, you should probably already be 1.0.0.

# Developing mobile applications
This section covers problems commonly encountered with:
* developing and distributing native mobile applications in JavaScript
* serving mobile users for web applications

I am seeking contributors for this section.

# Developing desktop applications
This section covers problems commonly encountered with developing and distributing desktop applications.

I am seeking contributors for this section.

## Cross platform framework
### Problem / Context
Deciding which cross platform framework to use is a waste of time.
### Recommended solution
Use [Electron](http://electron.atom.io/). It is now considered stable as version 1 was released on May 11, 2016. It is backed by the makers of GitHub and Atom, and has a strong community. Electron apps build and run on Mac, Windows, and Linux.

## Upcoming sections

* General problems
  * understanding event driven programming
  * Clustering (solution: throng)
  * Password hashing (solution: bcrypt)
  * Saving exact and secure dependency versions (solution: --save-exact, --secure, and .npmrc)
  * Good documentation / READMEs
  * Debug logging (solution: debug)
  * Event emitter (solution: eventemitter3)
  * testing
  * user analytics and app monitoring
  * other analytics: keen.io, google analytics and kissmetrics, and key metrics
  * npm publish scripts that update version number for you
  * promises and callbacks
  * error handling
* Developing for the web
  * Working with sockets (solution: socket.io)
  * Creating a REST API server (solution: Swagger)
  * Deploying serverless (solution: serverless and AWS Lambda
  * Application architecture (solution: single page apps with a back-end API server)
  * Handling server overload (solution: toobusy)
  * Rate limiting and prevent brute force logins
  * Authentication (solution: jsonwebtoken)
  * don't run your server on port 80 or 453
  * security
  * ssl
  * message queues and async function execution
* Developing mobile applications
  * immediate user feedback for server requests

## Contributing
Contributions are welcome through GitHub Issues! Please contribute by:

* asking for recommended solutions to your favorite problem
* offering recommended solutions to a problem in [Upcoming sections](#upcoming-sections) or in a GitHub Issue (please note the [criteria](#how-solutions-were-chosen) for recommended solutions)

## License

MIT License

Copyright (c) 2016 Faraz Syed

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
