# NX-依赖隔离



## 1、多应用软隔离

如果你在 `apps/` 目录下有两个应用 `a` 和 `b`，你希望它们使用不同的依赖（即“a 和 b 项目引用不同的库”），在 **Nx + Angular monorepo** 中完全可以做到，并且可以 **精确控制每个 app 能引用哪些 lib**。

------

## 🧭 举例结构

```bash
apps/
├── a/
│   └── project.json  // app a 的定义
├── b/
│   └── project.json  // app b 的定义
libs/
├── a/
│   └── feature1/     // 仅供 a 使用
├── b/
│   └── feature2/     // 仅供 b 使用
├── shared/
│   └── ui/           // 可共享使用
```

------

#### ✅ 步骤一：给项目打上 `tags`

每个库和 app 项目的 `project.json` 加上合适的 `tags`：

`apps/a/project.json`

```jsonc
{
  "name": "a",
  "tags": ["scope:a"]
}
```

`apps/b/project.json`

```jsonc
{
  "name": "b",
  "tags": ["scope:b"]
}
```

`libs/a/feature1/project.json`

```jsonc
{
  "name": "a-feature1",
  "tags": ["scope:a"]
}
```

`libs/b/feature2/project.json`

```jsonc
{
  "name": "b-feature2",
  "tags": ["scope:b"]
}
```

`libs/shared/ui/project.json`

```jsonc
{
  "name": "shared-ui",
  "tags": ["scope:shared"]
}
```

------

#### ✅ 步骤二：设置依赖约束规则（nx.json）

在根目录 `nx.json` 中加上以下规则：

```jsonc
{
  "projectGraph": {
    "dependencyConstraints": [
      {
        "sourceTag": "scope:a",
        "onlyDependOnLibsWithTags": ["scope:a", "scope:shared"]
      },
      {
        "sourceTag": "scope:b",
        "onlyDependOnLibsWithTags": ["scope:b", "scope:shared"]
      }
    ]
  }
}
```

这样就实现了：

| App    | 允许依赖                                |
| ------ | --------------------------------------- |
| `a`    | `scope:a`, `scope:shared`               |
| `b`    | `scope:b`, `scope:shared`               |
| ⛔ 禁止 | `a` 引用 `b` 的库，或 `b` 引用 `a` 的库 |

------

#### ✅ 步骤三：强制校验（使用 ESLint）

确保 `.eslintrc.json` 中启用了 `@nx/enforce-module-boundaries` 规则：

```json
{
  "rules": {
    "@nx/enforce-module-boundaries": [
      "error",
      {
        "enforceBuildableLibDependency": true,
        "depConstraints": [
          {
            "sourceTag": "scope:a",
            "onlyDependOnLibsWithTags": ["scope:a", "scope:shared"]
          },
          {
            "sourceTag": "scope:b",
            "onlyDependOnLibsWithTags": ["scope:b", "scope:shared"]
          }
        ]
      }
    ]
  }
}
```

------

#### ✅ 效果总结

| 场景                      | 是否允许 |
| ------------------------- | -------- |
| `a` app 引用 `a/feature1` | ✅ 允许   |
| `a` app 引用 `shared/ui`  | ✅ 允许   |
| `a` app 引用 `b/feature2` | ❌ 报错   |
| `b` app 引用 `b/feature2` | ✅ 允许   |
| `b` app 引用 `shared/ui`  | ✅ 允许   |
| `b` app 引用 `a/feature1` | ❌ 报错   |

------

## 📦 补充：npm 依赖也可以不同？

> 通常 monorepo 是共用一份 `package.json`，但：

- 你可以使用 [**Nx Plugin for Webpack Module Federation**](https://nx.dev/packages/angular/module-federation) 或微前端方式（每个 app 有独立依赖）
- 更常见的做法：让 app 引用各自的 lib，而不是直接引用 npm 包，把 npm 依赖封装进 lib（解耦 npm 层）

------



## 2、多应用依赖隔离

> ✅ 在 **Nx Monorepo 中**，让 `apps/a` 和 `apps/b` 各自拥有 **独立的 `package.json` 和依赖**。

这是一个**高级用法**，在 Nx 中不属于默认模式，但可以通过以下方式实现：

------

## 🧩 场景理解

| 模式                                       | 是否支持                                  |
| ------------------------------------------ | ----------------------------------------- |
| Nx 默认                                    | 所有项目共享一个根目录的 `package.json` ✅ |
| 每个 app 有自己的 `package.json`，依赖不同 | ❌ 默认不支持，需手动配置                  |

------

## ✅ 实现方式：**使用 Nx + NPM Workspace（或 PNPM Workspace）+ 自定义 package.json**

### 🚀 整体思路：

- Nx 继续管理项目结构和构建逻辑
- 每个 app 拥有自己的 `package.json`
- 根目录使用 npm/pnpm/yarn workspaces 管理子依赖
- 利用构建器或脚本确保每个 app 构建时只用它自己的依赖

------

## ✅ 示例结构

```
apps/
├── a/
│   ├── main.ts
│   └── package.json  ✅ 自己的依赖
├── b/
│   ├── main.ts
│   └── package.json  ✅ 自己的依赖
libs/
├── shared/
package.json          ✅ 根依赖，只包含 workspace 配置
nx.json
tsconfig.base.json
```

------

## ✅ 根目录 `package.json`

配置 NPM Workspace（也适用于 pnpm/yarn）：

```json
{
  "private": true,
  "workspaces": [
    "apps/a",
    "apps/b",
    "libs/**"
  ],
  "devDependencies": {
    "nx": "^18.0.0",
    "@nrwl/angular": "^18.0.0"
  }
}
```

> 安装时用 `npm install`，会自动装好所有子包依赖。

------

## ✅ 子项目的 `apps/a/package.json`

```json
{
  "name": "a",
  "version": "1.0.0",
  "dependencies": {
    "lodash": "^4.17.21",
    "@angular/core": "^16.0.0"
  }
}
```

## ✅ `apps/b/package.json`

```json
{
  "name": "b",
  "version": "1.0.0",
  "dependencies": {
    "moment": "^2.29.4",
    "@angular/core": "^16.0.0"
  }
}
```

> `a` 用 lodash，`b` 用 moment，完全分开。

------

## ✅ 启用并构建子 app

你要确保每个构建过程使用的是 app 自己的依赖。方法有两种：

### 方法一：使用 Nx `custom executor` 自定义构建流程

- 写一个 executor 来调用 app 的 `node_modules`
- 比如用 `npx --prefix apps/a ng build` 代替默认的 Nx 构建器

### 方法二：分离部署构建

- 构建前运行 `cd apps/a && npm install --production`
- 用 `vite`、`ng-packagr` 或自己写的 `build.ts` 脚本构建

------

## ⚠️ 注意事项

| 问题                                        | 说明                             |
| ------------------------------------------- | -------------------------------- |
| VSCode / TS 找不到依赖                      | 设置 `tsconfig.json` 中 `paths`  |
| 同一包多版本可能冲突                        | 推荐尽量版本对齐，或严格隔离环境 |
| 构建器默认用根目录依赖                      | 需重写 executor，或脚本方式      |
| `nx serve a` 不自动用 `apps/a/package.json` | 需手动配置运行逻辑               |

------

## 🔁 替代方案建议

如果你的目的只是 **逻辑上隔离不同 app 的依赖，而不是物理上分开**，那么更推荐：

- 所有依赖仍放在根 `package.json`
- a/b 通过 `libs/a-xxx` 和 `libs/b-xxx` 引入各自需要的包（再由 lib 引入 npm 包）
- 保持构建器和 `nx` 功能的完整性

------

## ✅ 总结：让 a、b 有独立依赖的方法

| 方法                                           | 可行性       | 复杂度 |
| ---------------------------------------------- | ------------ | ------ |
| Nx + npm workspaces + 每个 app 有 package.json | ✅ 可行       | 🟡 中高 |
| 根 `package.json` 管全局，lib 内封装依赖       | ✅ 推荐       | 🟢 中   |
| Nx 本身支持 per-project deps                   | ❌ 默认不支持 | 🔴      |

------

如果你想，我可以帮你写好根 `package.json` + 子 app 的 `package.json` + 自定义构建脚本，让你可以一键构建不同的项目。是否需要？