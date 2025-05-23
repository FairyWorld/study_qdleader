# 前端 package.json 中 scripts 的 中的常见属性

### preinstall

触发时机：在 npm 开始安装当前项目的依赖之前执行。
用途：通常用于执行一些必要的准备工作，比如设置环境变量，检查系统环境是否符合特定要求等。

### install

触发时机：在 npm install 命令执行时，这个脚本被触发。
用途：install 脚本通常是用来编译或构建项目。它可以被用作自动触发编译过程，例如对 TypeScript 项目进行编译或执行其他构建任务。不过，在实践中，install 通常不需要显式定义，因为 npm 默认行为已经涵盖了安装依赖的操作。

### postinstall

触发时机：在 npm 安装项目依赖后执行。
用途：这是最常用的脚本之一，用于在依赖安装完成后执行一些后处理操作，例如执行数据库迁移、本地化的构建脚本或者其他需要在依赖完全安装后执行的任务。
这些脚本在自动化和简化开发流程中扮演了重要的角色，可以显著提高开发效率和项目的可维护性。它们是自动化部署流程的重要组成部分，特别是在持续集成/持续部署 (CI/CD) 环境中。
