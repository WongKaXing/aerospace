# AeroSpace 配置文件说明 (翻译版)

---

## 基本配置

### config-version = 2
配置文件的版本号，用于保证兼容性和处理废弃项。如果省略，默认值为 1。

### after-startup-command = []
AeroSpace 启动后自动执行的命令列表。可用的命令详见：https://nikitabobko.github.io/AeroSpace/commands

### start-at-login = false
是否在登录系统时自动启动 AeroSpace。

### auto-reload-config = false
当配置文件被保存时，是否自动重新加载配置。设置为 `true` 之后，需要手动重新加载一次，自动重载才会开始生效。

---

## 布局归一化 (Normalization)

### enable-normalization-flatten-containers = true
启用容器展平归一化，自动清理嵌套容器中不必要的中间容器。

### enable-normalization-opposite-orientation-for-nested-containers = true
启用嵌套容器的反向方向归一化，允许嵌套容器使用与父容器相反的方向。

---

## 布局设置

### accordion-padding = 50
手风琴布局中，窗口之间的间距大小。设置为 0 可以禁用间距。

### default-root-container-layout = 'tiles'
默认的根容器布局模式。
- `tiles` — 平铺布局
- `accordion` — 手风琴布局

### default-root-container-orientation = 'auto'
默认的根容器方向（窗口分割方向）。
- `horizontal` — 水平分割
- `vertical` — 垂直分割
- `auto` — 自动：宽屏显示器使用水平方向，竖屏显示器使用垂直方向

---

## 焦点与鼠标

### on-focused-monitor-changed = ['move-mouse monitor-lazy-center']
当焦点所在的显示器发生变化时，自动将鼠标移动到新显示器的中心位置。如果不需要此行为，可以移除这一行（默认值为空数组 `[]`）。

### focus-follows-mouse.enabled = false
是否启用"鼠标跟随焦点"——鼠标移动到哪个窗口，焦点就切换到那个窗口。

### automatically-unhide-macos-hidden-apps = false
是否自动取消隐藏 macOS 中被隐藏的应用（Cmd+H 隐藏的应用）。如果经常误触 Cmd+H，可以开启此选项。详见：https://nikitabobko.github.io/AeroSpace/goodies#disable-hide-app

---

## 工作区设置

### persistent-workspaces = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]
持久化工作区列表。这些工作区即使没有任何窗口、不可见，也会保持存活，不会被自动关闭。此配置项仅在 `config-version = 2` 时可用。如果省略，默认值为空数组。

---

## 按键映射

### key-mapping.preset = 'qwerty'
键盘布局预设。
- `qwerty` — 标准 QWERTY 键盘
- `dvorak` — Dvorak 键盘
- `colemak` — Colemak 键盘

---

## 窗口间隙 (Gaps)

窗口之间的间隙 (inner) 和窗口与屏幕边缘之间的间隙 (outer)。

支持两种值格式：
- **常量**：`gaps.outer.top = 8`（所有显示器统一值）
- **按显示器设置**：`gaps.outer.top = [{ monitor.main = 16 }, { monitor."some-pattern" = 32 }, 24]`，其中最后的 `24` 是无匹配时的默认值。

```toml
gaps.inner.horizontal = 0   # 窗口之间的水平间隙
gaps.inner.vertical =   0   # 窗口之间的垂直间隙
gaps.outer.left =       0   # 屏幕左侧外边距
gaps.outer.bottom =     0   # 屏幕底部外边距
gaps.outer.top =        0   # 屏幕顶部外边距
gaps.outer.right =      0   # 屏幕右侧外边距
```

---

## 绑定模式 (Binding Modes)

AeroSpace 支持多种绑定模式，允许同一组快捷键在不同的模式下有不同的功能。

### on-mode-changed = []
每当绑定模式改变时执行的回调命令列表。

---

## 主模式 (main) 快捷键绑定

`main` 模式是必须存在的基础绑定模式。

### 可用的按键:
- **字母**：a-z
- **数字**：0-9
- **小键盘数字**：keypad0-keypad9
- **F 功能键**：f1-f20
- **特殊按键**：minus, equal, period, comma, slash, backslash, quote, semicolon, backtick, leftSquareBracket, rightSquareBracket, space, enter, esc, backspace, tab, pageUp, pageDown, home, end, forwardDelete, sectionSign（仅限 ISO/欧式键盘）
- **小键盘特殊键**：keypadClear, keypadDecimalMark, keypadDivide, keypadEnter, keypadEqual, keypadMinus, keypadMultiply, keypadPlus
- **方向键**：left, down, up, right

### 可用的修饰键：cmd, alt, ctrl, shift

### 主模式绑定说明：

| 快捷键 | 命令 | 功能说明 |
|--------|------|----------|
| `alt-slash` | `layout tiles horizontal vertical` | 切换平铺布局（水平/垂直） |
| `alt-comma` | `layout accordion horizontal vertical` | 切换手风琴布局（水平/垂直） |
| `alt-h` | `focus left` | 聚焦到左边的窗口 |
| `alt-j` | `focus down` | 聚焦到下边的窗口 |
| `alt-k` | `focus up` | 聚焦到上边的窗口 |
| `alt-l` | `focus right` | 聚焦到右边的窗口 |
| `alt-shift-h` | `move left` | 将当前窗口向左移动 |
| `alt-shift-j` | `move down` | 将当前窗口向下移动 |
| `alt-shift-k` | `move up` | 将当前窗口向上移动 |
| `alt-shift-l` | `move right` | 将当前窗口向右移动 |
| `alt-minus` | `resize smart -50` | 将窗口缩小 50 单位 |
| `alt-equal` | `resize smart +50` | 将窗口放大 50 单位 |
| `alt-1` ~ `alt-9` | `workspace 1` ~ `workspace 9` | 切换到工作区 1~9 |
| `alt-shift-1` ~ `alt-shift-9` | `move-node-to-workspace 1` ~ `9` | 将当前窗口移动到工作区 1~9 |
| `alt-tab` | `workspace-back-and-forth` | 在当前和上一个工作区之间切换 |
| `alt-shift-tab` | `move-workspace-to-monitor --wrap-around next` | 将当前工作区移动到下一个显示器 |
| `alt-shift-semicolon` | `mode service` | 进入 service 模式 |

> 被注释掉的 alt-a ~ alt-z 和 alt-shift-a ~ alt-shift-z 分别对应切换到和移动窗口到字母命名的工作区，可按需取消注释。

---

## 服务模式 (service) 快捷键绑定

`service` 模式用于系统管理操作，按 `alt-shift-semicolon` 进入。每个操作执行完后自动回到 `main` 模式。

| 快捷键 | 命令 | 功能说明 |
|--------|------|----------|
| `esc` | `reload-config, mode main` | 重新加载配置，回到主模式 |
| `r` | `flatten-workspace-tree, mode main` | 重置工作区布局（展平窗口树） |
| `f` | `layout floating tiling, mode main` | 在浮动布局和平铺布局之间切换 |
| `backspace` | `close-all-windows-but-current, mode main` | 关闭除当前窗口外的所有窗口 |
| `alt-shift-h` | `join-with left, mode main` | 将当前窗口与左边窗口合并 |
| `alt-shift-j` | `join-with down, mode main` | 将当前窗口与下方窗口合并 |
| `alt-shift-k` | `join-with up, mode main` | 将当前窗口与上方窗口合并 |
| `alt-shift-l` | `join-with right, mode main` | 将当前窗口与右边窗口合并 |

> 被注释掉的 `s` 绑定（sticky 布局）等待此功能的实现：https://github.com/nikitabobko/AeroSpace/issues/2
> 被注释掉的 `alt-enter` 绑定展示如何通过 `exec-and-forget` 启动终端应用（类似 i3 的行为）。

---

## 相关链接

- 命令参考：https://nikitabobko.github.io/AeroSpace/commands
- 配置指南：https://nikitabobko.github.io/AeroSpace/guide
- GitHub 仓库：https://github.com/nikitabobko/AeroSpace
