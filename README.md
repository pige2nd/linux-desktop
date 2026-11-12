# linux-desktop

Ubuntu 26.04 的 Niri 桌面配置与部署：普通 Niri 使用 DMS；独立 NyxNiri 会话使用 Noctalia。包括 Vicinae、Fcitx5/Rime、Xresources、WeChat desktop 覆盖、会话启动器、补丁、种子与测试。

配置所有权和会话边界见 [ARCHITECTURE.md](docs/ARCHITECTURE.md)，依赖安装与新机步骤见 [MIGRATION.md](docs/MIGRATION.md)。`install.sh` 会部署配置、复制 DMS/Fcitx5 种子并启用桌面服务，请按迁移文档执行。

```sh
git clone https://github.com/pige2nd/linux-desktop.git ~/linux-desktop
cd ~/linux-desktop
# 先按 docs/MIGRATION.md 安装依赖与补丁，再运行：
./install.sh
./scripts/install-nyxniri-system.sh
./tests/verify-desktop.sh
```

WezTerm 仍是桌面的外部终端程序依赖，其配置位于 [wezterm-config](https://github.com/pige2nd/wezterm-config)。Zsh、tmux、Yazi、Neovim 位于 [dotfiles](https://github.com/pige2nd/dotfiles)，本仓库不部署它们。

## 从旧 dotfiles 切换

在旧 dotfiles 目录仍完整时，先注销 Niri/NyxNiri 并从 TTY 或其他桌面执行：

```sh
cd ~/dotfiles
stow --no-folding --target="$HOME" --delete niri niri-nyxniri noctalia session vicinae xresources systemd im rime applications
```

之后在本仓库按迁移文档重新部署并验证，再更新旧 dotfiles。不要手动删除仍指向旧仓库的配置。DMS/Fcitx5 是复制种子；沿用原安装脚本行为，部署前需备份本机修改。已有 Noctalia config.toml 会保留。

## 本地回归检查

```sh
./tests/test-compact-status-bars.sh
./tests/test-noctalia-plugins.sh
./tests/test-toggle-eyecare.sh
./tests/test-nyxniri-session.sh
```

`verify-desktop.sh` 和 `test-session-discoverable.sh` 需要已部署的真实 Linux 桌面。

来源：[dotfiles@984d8af](https://github.com/pige2nd/dotfiles/tree/984d8af24312fc064894a35bc50e7287db6ea641)。新仓库从此次快照开始，之前的历史保留在来源仓库。
