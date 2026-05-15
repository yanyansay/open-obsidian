# open-obsidian

[中文](./README.md)

A tiny macOS terminal command for opening local folders with Obsidian.

```sh
ob [folder]
```

If no path is provided, `ob` opens the current directory.

## Install

Clone this repo and link `ob` into a directory on your `PATH`:

```sh
git clone https://github.com/yanyansay/open-obsidian.git
cd open-obsidian
chmod +x ob
ln -sf "$PWD/ob" ~/.local/bin/ob
```

Make sure `~/.local/bin` is already on your `PATH`:

```sh
echo $PATH
```

## Usage

Open the current directory:

```sh
ob
```

Open a specific folder:

```sh
ob ~/Documents/my-vault
```

The given path is resolved to an absolute path before being opened.

## Obsidian App Name

By default, the command uses the macOS app name `Obsidian`:

```sh
open -a Obsidian /path/to/folder
```

If your Obsidian app name is different, set `OB_OBSIDIAN_APP`:

```sh
OB_OBSIDIAN_APP="Obsidian" ob ~/Documents/my-vault
```

## Output

After opening with Obsidian:

```text
✅ 已用 Obsidian 打开: /path/to/folder
```

If Obsidian is not found:

```text
⚠️ 没找到 Obsidian，请先安装 Obsidian，或用 OB_OBSIDIAN_APP 指定应用名。
```

If the target path does not exist:

```text
ob: path does not exist: missing-folder
```

If the target is not a folder:

```text
ob: path is not a folder: README.md
```

## Uninstall

Remove the command link:

```sh
rm ~/.local/bin/ob
```

You can also delete the cloned repo if you no longer need it.

## License

MIT
