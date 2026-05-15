# open-obsidian

[English](./README.en.md)

一个极小的 macOS 终端命令，用来从任意目录快速用 Obsidian 打开本地文件夹。

```sh
ob [文件夹]
```

如果不传路径，`ob` 会打开当前目录。

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

## Obsidian 应用名

默认使用 macOS 应用名 `Obsidian`：

```sh
open -a Obsidian /path/to/folder
```

如果你的 Obsidian 应用名不同，可以用 `OB_OBSIDIAN_APP` 指定：

```sh
OB_OBSIDIAN_APP="Obsidian" ob ~/Documents/my-vault
```

## 输出提示

成功用 Obsidian 打开后：

```text
✅ 已用 Obsidian 打开: /path/to/folder
```

如果没有找到 Obsidian：

```text
⚠️ 没找到 Obsidian，请先安装 Obsidian，或用 OB_OBSIDIAN_APP 指定应用名。
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
