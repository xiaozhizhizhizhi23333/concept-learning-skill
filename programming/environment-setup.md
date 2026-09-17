# 本地 Python 数据分析环境搭建记录

> 搭建日期：2026-09-17
> 环境：Windows 11（10.0.26100）· 64 位
> 目标：为一套「零基础 → Python 数据分析与可视化」的学习计划准备可用的本地环境

本文记录本机开发环境的**完整配置、验证方式，以及搭建过程中遇到的网络问题与解决办法**。换电脑或环境损坏时，可以照此重建。

---

## 一、最终环境清单

| 组件 | 版本 | 安装位置 |
|---|---|---|
| Python | **3.12.10**（系统内唯一版本） | `%LOCALAPPDATA%\Programs\Python\Python312` |
| pip | 25.0.1 | 随 Python 安装 |
| pip 镜像源 | 清华 TUNA（主）+ 阿里云（备用） | `%APPDATA%\pip\pip.ini` |
| VS Code | **1.138.0** | `%LOCALAPPDATA%\Programs\Microsoft VS Code` |
| Jupyter 内核 | `python312`（显示名 Python 3.12） | `%APPDATA%\jupyter\kernels\python312` |

### 已装的 VS Code 扩展（共 6 个）

| 扩展 | 版本 | 作用 |
|---|---|---|
| `ms-ceintl.vscode-language-pack-zh-hans` | 1.131.2026090407 | 简体中文界面 |
| `ms-python.python` | 2026.7.2026082601 | Python 语言支持 |
| `ms-toolsai.jupyter` | 2026.6.2026071501 | **支持 .ipynb 笔记本** |
| `ms-toolsai.jupyter-keymap` | 1.1.2 | Jupyter 快捷键（依赖项） |
| `ms-toolsai.jupyter-renderers` | 1.3.2025062701 | 输出渲染（依赖项） |
| `ms-toolsai.vscode-jupyter-cell-tags` | 0.1.9 | 单元格标签（依赖项） |

### 已装的关键 Python 包

`ipykernel` 7.3.0 · `ipython` 9.17.1 · `numpy` 2.5.3 · `pandas` 3.0.5 · `matplotlib` 3.11.2 · `nbconvert` 7.17.1

---

## 二、安装步骤

### 1. 安装 Python 3.12

先确认系统里没有其他 Python 版本（避免多版本冲突）：

```bash
py --list                       # 查看 py launcher 识别的所有版本
where python                    # 查看 PATH 中的 python 位置
```

下载并静默安装（用户级安装，不需要管理员权限）：

```powershell
$installer = "$env:USERPROFILE\Downloads\python-install\python-3.12.10-amd64.exe"
$args = @("/quiet", "InstallAllUsers=0", "PrependPath=1",
          "Include_test=0", "Include_launcher=1", "InstallLauncherAllUsers=0",
          "AssociateFiles=1", "Shortcuts=1")
Start-Process -FilePath $installer -ArgumentList $args -Wait
```

关键参数说明：

- `InstallAllUsers=0` — 装到当前用户目录，免管理员权限
- `PrependPath=1` — 自动加入 PATH，且优先级高于 Windows 应用商店的占位符
- `Include_launcher=1` — 安装 `py` 启动器

### 2. 配置 pip 国内镜像源

新建 `%APPDATA%\pip\pip.ini`：

```ini
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
extra-index-url = https://mirrors.aliyun.com/pypi/simple/
trusted-host = pypi.tuna.tsinghua.edu.cn
               mirrors.aliyun.com

[install]
timeout = 120
```

### 3. 安装 VS Code

```powershell
$installer = "$env:USERPROFILE\Downloads\vscode-install\VSCodeUserSetup-x64.exe"
$args = @("/VERYSILENT", "/NORESTART",
          "/MERGETASKS=!runcode,addcontextmenufiles,addcontextmenufolders,associatewithfiles,addtopath")
Start-Process -FilePath $installer -ArgumentList $args -Wait
```

### 4. 装扩展并注册 Jupyter 内核

```bash
# 注册内核，让 VS Code 能选到 Python 3.12
python -m ipykernel install --user --name python312 --display-name "Python 3.12"
```

设置中文界面：编辑 `%USERPROFILE%\.vscode\argv.json`，加入

```json
"locale": "zh-cn"
```

> 注意：语言必须在 `argv.json` 里设置，写在用户 `settings.json` 里不生效。改完要**完全重启** VS Code。

---

## 三、验证方式（如何确认环境可用）

### 1. 确认 Python 版本唯一

```bash
where python                    # 应只指向 Python312\python.exe
python --version                # 应为 Python 3.12.10
```

同时检查注册表与常见安装目录，确认没有第二个版本：

```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*",
                 "HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" -ErrorAction SilentlyContinue |
  Where-Object { $_.DisplayName -match '^Python' } |
  Select-Object DisplayName, DisplayVersion
```

**本机验证结果**：仅 `Python 3.12.10 (64-bit)` 一个版本。

### 2. 确认 pip 走的是国内源

```bash
pip config list                 # 查看生效的镜像配置
pip install requests            # 观察输出中是否出现镜像站域名
```

**本机验证结果**：输出显示下载源为 `mirrors.aliyun.com`，5 个依赖包秒级装完。

### 3. 确认 .ipynb 能真正跑通

用命令行实际执行一遍 notebook（不是「打开看看」，是真的跑）：

```bash
python -m nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=180 "环境测试.ipynb"
```

**本机验证结果**：`notebooks/环境测试.ipynb` 的 5 个代码块全部执行成功，包含文字输出与 PNG 图表输出。

---

## 四、遇到的问题与解决办法

### 问题 1：Python 官网 3.12 系列没有对应的 Windows 安装包

**现象**：下载 `python-3.12.14-amd64.exe` 返回 404。

**原因**：Python 官网 FTP 上，3.12 系列的**最新小版本（3.12.14）只提供源码包**，Windows 安装程序只对部分版本发布。

**解决**：逐个探测有安装包的版本，最终选用 **3.12.10**（3.12 系列中带 Windows 安装程序的最新版本）。探测命令：

```bash
for v in 3.12.10 3.12.9 3.12.8; do
  curl -s "https://www.python.org/ftp/python/$v/" | grep -oE "python-$v-amd64\.exe"
done
```

### 问题 2：VS Code 扩展市场无法访问

**现象**：`code --install-extension ms-python.python` 反复失败；`marketplace.visualstudio.com` 的 POST 请求全部被重置。

**原因**：本机网络拦截了扩展市场的 API 通道，但扩展文件的 CDN 域名可用。

**解决**：改为**离线安装**，三步走：

1. 用 GET 访问扩展详情页（该通道时通时断，需要循环重试 5–20 次）：

   ```bash
   curl -s "https://marketplace.visualstudio.com/items?itemName=ms-python.python" -o page.html
   ```

2. 从返回的 HTML 中提取 CDN 路径片段：

   ```
   ms-python.gallerycdn.vsassets.io/extensions/ms-python/python/2026.7.2026082601/1787741724831/Microsoft.VisualStudio.Services.Icons.Default
   ```

   把末尾的 `Microsoft.VisualStudio.Services.Icons.Default` 替换为 `Microsoft.VisualStudio.Services.VSIXPackage`，即为安装包真实地址。

3. 下载后用命令行离线安装：

   ```bash
   code --install-extension "./ms-python.python.vsix" --force
   ```

> 提示：Jupyter 扩展还有 3 个依赖扩展（`jupyter-keymap` / `jupyter-renderers` / `vscode-jupyter-cell-tags`），需要按同样方式一并下载安装，否则 .ipynb 无法正常运行。

### 问题 3：pip 批量安装被中断

**现象**：一次安装 `jupyter ipykernel pandas matplotlib` 时进程被中断。

**原因**：环境注入的临时文件清理防护机制（`sitecustomize.py`）在 pip 清理临时目录时误触发。

**解决**：加 `--no-cache-dir` 关闭缓存，并**分批安装**（先装核心的 `ipykernel`，再装其余），必要时放到后台执行避免超时。

---

## 五、日常使用提示

1. 第一次打开 `.ipynb` 文件时，点右上角**「选择内核」→ 选 `Python 3.12`**，选一次就会记住。
2. 本机**不能直接在 VS Code 里搜索安装新扩展**（见问题 2）。需要装扩展时，用上面的离线方式处理。
3. Python 的**报错信息始终是英文**，这与编辑器语言无关，是 Python 语言本身的输出。
