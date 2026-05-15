# open-obsidian

[English](./README.en.md)

一个极小的 macOS 终端命令，用来从任意目录快速用 Obsidian 打开本地文件夹。

```sh
ob [文件夹]
```

如果不传路径，`ob` 会打开当前目录。

## 运行环境

`open-obsidian` 目前只面向 macOS：

- macOS，脚本依赖系统自带的 `zsh`、`open` 和 `osascript`。
- 已安装 Obsidian，并且应用位于 `/Applications/Obsidian.app`、`~/Applications/Obsidian.app`，或已被 macOS 注册为 `Obsidian`。
- 终端可以执行 `zsh` 脚本。
- 手动安装需要 `git`，并且建议把 `~/.local/bin` 加入 `PATH`。

当前版本在 macOS + Obsidian 1.12.7 环境下验证过。其他 Obsidian 版本只要继续使用相同的本地 vault 配置格式，一般也可以工作。

如果电脑上没有安装 Obsidian，执行 `ob` 会提示：

```text
⚠️ 没找到 Obsidian，请先安装 Obsidian。
```

## 安装

克隆仓库，并把 `ob` 链接到你的 `PATH` 目录里：

```sh
git clone https://github.com/yanyansay/open-obsidian.git
cd open-obsidian
chmod +x ob
ln -sf "$PWD/ob" ~/.local/bin/ob
```

确认 `~/.local/bin` 已经在 `PATH` 中：

```sh
echo $PATH
```

## 使用

打开当前目录：

```sh
ob
```

打开指定文件夹：

```sh
ob ~/Documents/my-vault
```

传入的路径会先解析成绝对路径，再交给 Obsidian 打开。

## 打开方式

`ob` 会先把目标文件夹登记到 Obsidian 的本地 vault 列表，再用 Obsidian URL scheme 打开对应 vault ID：

```sh
obsidian://open?vault=<vault-id>
```

这样可以让 Obsidian 明确打开传入的文件夹，而不是只启动应用，也不会遇到 `path` 找不到已知 vault 的问题。

如果目标文件夹还不是 Obsidian 已知 vault，`ob` 会先退出 Obsidian，再登记并重新打开它。这是为了避免 Obsidian 运行中回写配置，覆盖新登记的 vault。

登记 vault 时，`ob` 会更新这个文件：

```text
~/Library/Application Support/obsidian/obsidian.json
```

Obsidian 打开目标文件夹后，可能会在该文件夹下创建 `.obsidian/` 配置目录。这是 Obsidian 自己保存 vault 设置的目录，不是 `ob` 的源码文件。

## 输出提示

成功用 Obsidian 打开后：

```text
✅ 已用 Obsidian 打开: /path/to/folder
```

如果没有找到 Obsidian：

```text
⚠️ 没找到 Obsidian，请先安装 Obsidian。
```

如果目标路径不存在：

```text
ob: path does not exist: missing-folder
```

如果目标不是文件夹：

```text
ob: path is not a folder: README.md
```

## 卸载

删除命令链接：

```sh
rm ~/.local/bin/ob
```

如果不再需要，也可以删除克隆下来的仓库。

## 许可证

MIT
