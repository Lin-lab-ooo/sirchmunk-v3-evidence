# 手动上传GitHub

建议仓库名：`sirchmunk-v3-evidence`。建议简介：

> Experimental budgeted graph evidence selection for a pinned Sirchmunk DEEP workflow, with paired HotpotQA measurements and reproducible offline tests.

## 上传内容

1. 解压本次交付ZIP，打开里面的 `sirchmunk-v3-release`。
2. 新建空GitHub仓库，或在你自行选择的仓库中使用 **Add file → Upload files**。
3. 将发布目录内的文件和子目录拖入上传区，保留目录层级。确认根目录有 `README.md`、`README.zh-CN.md`、`LICENSE`、`pyproject.toml` 和 `.gitignore`，以及隐藏的 `.github` 目录。
4. 建议提交说明：`Publish V3 research code and paired baseline results`。
5. 提交后检查README图表、相对链接和CI。ZIP可另作为Release附件；源码页面应包含解压后的文件树。

GitHub网页一次支持最多100个文件、每文件25MiB；具体上传操作见[官方说明](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)。若浏览器没有保留隐藏文件，请单独补充 `.gitignore` 和 `.github/workflows/core.yml`。

## 此包的发布边界

只使用本次经过审核的发布目录与ZIP。它已排除私人账本、账户回执、密钥、本机配置、原始数据、问答文本、原始模型轨迹、模型缓存、其他实验版本及Git历史。压缩包的校验值和逐文件清单供你核对实际文件是否改变。

本次整理没有上传GitHub，也没有发起新的付费模型调用。公开包保留所有V3测量失败和一次请求预算中断，不把成绩不好的题删除。

## 发布文案

可以写：

> 两批不同共享语料的80题描述性合并中，V3的EM为42/80，适配原生DEEP为40/80；V3总token减少18.1%，完整支持来源读取增加，但耗时略高。代码、匿名逐题指标、复算脚本和局限已公开。

同时注明：精确配对检验p=0.6875，尚未证明整体优势；不是未修改FAST或LENS完整复现。两批不同语料规模和采样历史分别报告。价格估算不是账单，完整来源命中不是语义正确性证明。

发布前保留MIT许可证、两份Apache 2.0许可证和第三方声明，确认README里的统计仍能通过 `python -B scripts/recompute_results.py --check`。不要将旧项目根目录或私人结果目录整体拖入GitHub。
