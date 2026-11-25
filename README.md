# Megatron-LM 与 Megatron Core 版本对照

[releases/](releases/) 收录了 31 个源码快照。可按 tag 查看 [GPU 依赖](#各版本的-gpu-依赖)、[源码安装约束](#源码安装约束) 和 [逐版变更](#逐版新增特性与修复)。`v2.5` 和 `23.04` 是 Megatron-LM 的历史标签。`23.04` 随附的 Core 包版本为 `0.1.0`，从 `core_v0.4.0` 起按 Core 版本号排列。[23.04 包版本](releases/23.04/megatron/core/package_info.py)

## 各版本的 GPU 依赖

**NGC** 列是该 tag 的测试环境或 CI 的 dev 基础镜像，链接指向 NVIDIA 对应月份的 PyTorch 容器说明。五个组件列采用 Linux x86-64 镜像配置中的版本，并计入下文列出的 dev Dockerfile 覆盖。PyTorch 保留 NGC 构建号（`a0+` 后为提交缩写）。TE 是 NVIDIA Transformer Engine，取基础镜像、CI 指定的源码提交或该 tag 的 `uv.lock`。这些值用于复现环境。单独用 pip 安装时的约束见下一节。

| Megatron tag | NGC | PyTorch | CUDA | NCCL | cuDNN | cuBLAS | TE | 快照依据 |
|---|---|---|---|---|---|---|---|---|
| [`v2.5`](releases/v2.5/) | [20.12](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel_20-12.html) | 1.8.0a0+1606899 | 11.1.1.002 | 2.8.3 | 8.0.5.43 | 11.3.0.106 | — | [实测](releases/v2.5/README.md) |
| [`23.04`](releases/23.04/) | [22.12](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-22-12.html) | 1.14.0a0+410ce96 | 11.8.0.065 | 2.15.5 | 8.7.0.84 | 11.11.3.6 | 0.3 | [CI](releases/23.04/.gitlab-ci.yml) |
| [`core_v0.4.0`](releases/core_v0.4.0/) | [23.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-04.html) | 2.1.0a0+fe05266 | 12.1.0.023 | 2.17.1 | 8.9.0.131 | 12.1.3.1 | 0.7 | [CI](releases/core_v0.4.0/.gitlab-ci.yml) |
| [`core_v0.5.0`](releases/core_v0.5.0/) | [23.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-04.html) | 2.1.0a0+fe05266 | 12.1.0.023 | 2.17.1 | 8.9.0.131 | 12.1.3.1 | 0.7 | [CI](releases/core_v0.5.0/.gitlab-ci.yml) |
| [`core_v0.6.0`](releases/core_v0.6.0/) | [23.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-04.html) | 2.1.0a0+fe05266 | 12.1.0.023 | 2.17.1 | 8.9.0.131 | 12.1.3.1 | 0.7 | [CI](releases/core_v0.6.0/.gitlab-ci.yml) |
| [`core_v0.7.0`](releases/core_v0.7.0/) | [23.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-04.html) | 2.1.0a0+fe05266 | 12.1.0.023 | 2.17.1 | 8.9.0.131 | 12.1.3.1 | 0.7 | [CI](releases/core_v0.7.0/.gitlab-ci.yml) |
| [`core_r0.8.0`](releases/core_r0.8.0/) | [24.01](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-24-01.html) | 2.2.0a0+81ea7a4 | 12.3.2.001 | 2.19.4 | 8.9.7.29+cuda12.2 | 12.3.4.1 | 1.2 | [CI](releases/core_r0.8.0/.gitlab-ci.yml) |
| [`core_r0.9.0`](releases/core_r0.9.0/) | [24.01](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-24-01.html) | 2.2.0a0+81ea7a4 | 12.3.2.001 | 2.19.4 | 8.9.7.29+cuda12.2 | 12.3.4.1 | 1.2 | [CI](releases/core_r0.9.0/.gitlab/stages/01.tests.yml) |
| [`core_r0.10.0`](releases/core_r0.10.0/) | [24.07](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-24-07.html) | 2.4.0a0+3bcc3cd | 12.5.1.007 | 2.22.3 | 9.2.1.18 | 12.5.3.2 | 1.8 | [CI](releases/core_r0.10.0/.gitlab/stages/01.test.yml) |
| [`v0.11.0`](releases/v0.11.0/) | [24.10](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-24-10.html) | 2.5.0a0+e000cf0 | 12.6.2.004 | 2.22.3 | 9.5.0.50 | 12.6.3.3 | 1.11 | [CI](releases/v0.11.0/.gitlab/stages/01.test.yml) |
| [`core_v0.12.0`](releases/core_v0.12.0/) | [25.03](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-03.html) | 2.7.0a0+7c8ec84 | 12.8.1.012 | 2.25.1 | 9.8.0.87 | 12.8.4.1 | 2.2.0.dev0+bee4649c | [CI](releases/core_v0.12.0/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.12.0/Dockerfile.ci.dev) |
| [`core_v0.12.1`](releases/core_v0.12.1/) | [25.03](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-03.html) | 2.7.0a0+7c8ec84 | 12.8.1.012 | 2.25.1 | 9.8.0.87 | 12.8.4.1 | 2.2.0.dev0+bee4649c | [CI](releases/core_v0.12.1/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.12.1/Dockerfile.ci.dev) |
| [`core_v0.12.2`](releases/core_v0.12.2/) | [25.03](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-03.html) | 2.7.0a0+7c8ec84 | 12.8.1.012 | 2.25.1 | 9.8.0.87 | 12.8.4.1 | 2.2.0.dev0+bee4649c | [CI](releases/core_v0.12.2/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.12.2/Dockerfile.ci.dev) |
| [`core_v0.12.3`](releases/core_v0.12.3/) | [25.03](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-03.html) | 2.7.0a0+7c8ec84 | 12.8.1.012 | 2.25.1 | 9.8.0.87 | 12.8.4.1 | 2.2.0.dev0+bee4649c | [CI](releases/core_v0.12.3/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.12.3/Dockerfile.ci.dev) |
| [`core_v0.13.0`](releases/core_v0.13.0/) | [25.05](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-05.html) | 2.8.0a0+5228986 | 12.9.0.043 | 2.26.5 | 9.10.1.4 | 12.9.0.13 | 2.5.0+8382eed6 | [CI](releases/core_v0.13.0/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.13.0/docker/Dockerfile.ci.dev) |
| [`core_v0.13.1`](releases/core_v0.13.1/) | [25.05](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-05.html) | 2.8.0a0+5228986 | 12.9.0.043 | 2.26.5 | 9.10.1.4 | 12.9.0.13 | 2.5.0+8382eed6 | [CI](releases/core_v0.13.1/.gitlab/stages/01.build.yml) · [TE](releases/core_v0.13.1/docker/Dockerfile.ci.dev) |
| [`core_v0.14.0`](releases/core_v0.14.0/) | [25.06](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-06.html) | 2.8.0a0+5228986 | 12.9.1.010 | 2.27.3 | 9.10.2.21 | 12.9.1.4 | 2.7.0 | [CI](releases/core_v0.14.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.14.0/uv.lock) |
| [`core_v0.15.0`](releases/core_v0.15.0/) | [25.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-09.html) | 2.9.0a0+50eac81 | 13.0.1.012 | 2.27.7 | 9.13.0.50 | 13.0.2.14 | 2.9.0+70f53666 | [CI](releases/core_v0.15.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.15.0/uv.lock) |
| [`core_v0.15.1`](releases/core_v0.15.1/) | [25.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-09.html) | 2.9.0a0+50eac81 | 13.0.1.012 | 2.27.7 | 9.13.0.50 | 13.0.2.14 | 2.9.0+70f53666 | [CI](releases/core_v0.15.1/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.15.1/uv.lock) |
| [`core_v0.15.2`](releases/core_v0.15.2/) | [25.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-09.html) | 2.9.0a0+50eac81 | 13.0.1.012 | 2.27.7 | 9.13.0.50 | 13.0.2.14 | 2.9.0+70f53666 | [CI](releases/core_v0.15.2/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.15.2/uv.lock) |
| [`core_v0.15.3`](releases/core_v0.15.3/) | [25.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-09.html) | 2.9.0a0+50eac81 | 13.0.1.012 | 2.27.7 | 9.13.0.50 | 13.0.2.14 | 2.9.0+70f53666 | [CI](releases/core_v0.15.3/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.15.3/uv.lock) |
| [`core_v0.16.0`](releases/core_v0.16.0/) | [25.11](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-11.html) | 2.10.0a0+b558c98 | 13.0.2.006 | 2.28.8 | 9.15.0.58 | 13.1.0.3 | 2.12.0+5671fd36 | [CI](releases/core_v0.16.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.16.0/uv.lock) |
| [`core_v0.16.1`](releases/core_v0.16.1/) | [25.11](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-11.html) | 2.10.0a0+b558c98 | 13.0.2.006 | 2.28.8 | 9.15.0.58 | 13.1.0.3 | 2.12.0+5671fd36 | [CI](releases/core_v0.16.1/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.16.1/uv.lock) |
| [`core_v0.17.0`](releases/core_v0.17.0/) | [26.02](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-02.html) | 2.11.0a0+eb65b36 | 13.1.1.006 | 2.29.stable.20260109 | 9.19.0.56 | 13.2.1.1 | 2.14.0+71bbefbf | [CI](releases/core_v0.17.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.17.0/uv.lock) |
| [`core_v0.17.1`](releases/core_v0.17.1/) | [26.02](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-02.html) | 2.11.0a0+eb65b36 | 13.1.1.006 | 2.29.stable.20260109 | 9.19.0.56 | 13.2.1.1 | 2.14.1+366798ef | [CI](releases/core_v0.17.1/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.17.1/uv.lock) |
| [`core_v0.18.0`](releases/core_v0.18.0/) | [26.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-04.html) | 2.12.0a0+0291f96 | 13.2.1.009 | 2.29.7 | 9.21.0.82 | 13.4.0.1 | 2.16.0+4220403e | [CI](releases/core_v0.18.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.18.0/uv.lock) |
| [`core_v0.18.2`](releases/core_v0.18.2/) | [26.04](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-04.html) | 2.12.0a0+0291f96 | 13.2.1.009 | 2.29.7 | 9.21.0.82 | 13.4.0.1 | 2.16.0+b9d690e0 | [CI](releases/core_v0.18.2/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.18.2/uv.lock) |
| [`core_v0.19.0`](releases/core_v0.19.0/) | [26.06](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-06.html) | 2.13.0a0+8145d63 | 13.3.0.035 | 2.30.7-1+cuda13.3 | 9.23.0.39 | 13.5.1.27 | 2.17.1+4329ff84 | [CI](releases/core_v0.19.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.19.0/uv.lock) · [NCCL](releases/core_v0.19.0/docker/Dockerfile.ci.dev) |
| [`core_v0.19.2`](releases/core_v0.19.2/) | [26.06](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-06.html) | 2.13.0a0+8145d63 | 13.3.0.035 | 2.30.7-1+cuda13.3 | 9.23.0.39 | 13.5.1.27 | 2.18.0+27486e03 | [CI](releases/core_v0.19.2/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.19.2/uv.lock) · [NCCL](releases/core_v0.19.2/docker/Dockerfile.ci.dev) |
| [`core_v0.20.0`](releases/core_v0.20.0/) | [26.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-09.html) | 2.14.0a0+b2c75dd | 13.4.1.012 | 2.31.2 | 9.26.0.51 | 13.8.1.7 | 2.20.2+44f31bbe | [CI](releases/core_v0.20.0/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.20.0/uv.lock) · [cuBLAS](releases/core_v0.20.0/docker/Dockerfile.ci.dev) |
| [`core_v0.20.1`](releases/core_v0.20.1/) | [26.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-26-09.html) | 2.14.0a0+b2c75dd | 13.4.1.012 | 2.31.2 | 9.26.0.51 | 13.8.1.7 | 2.21.0+7457e47d | [CI](releases/core_v0.20.1/.gitlab/stages/01.build.yml) · [锁文件](releases/core_v0.20.1/uv.lock) · [cuBLAS](releases/core_v0.20.1/docker/Dockerfile.ci.dev) |

### 其他测试环境与版本差异

| 适用范围 | 测试环境 | NGC | PyTorch | CUDA | NCCL | cuDNN | cuBLAS |
|---|---|---|---|---|---|---|---|
| 0.4.0 | 部分 GPT、T5 等功能测试 | [23.07](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-07.html) | 2.1.0a0+b5021ba | 12.1.1.009 | 2.18.3 | 8.9.3.28 | 12.1.3.1 |
| 0.4.0 | 上下文并行专用镜像的基础版本（另含 FlashAttention 1.0.9） | [23.10](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-10.html) | 2.1.0a0+32f93b1 | 12.2.2.009 | 2.19.3 | 8.9.5.29 | 12.2.5.6 |
| 0.10.0 至 0.15.3 | LTS 基础镜像 | [24.01](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-24-01.html) | 2.2.0a0+81ea7a4 | 12.3.2.001 | 2.19.4 | 8.9.7.29+cuda12.2 | 12.3.4.1 |
| 0.16.0 至 0.20.1 | LTS 基础镜像 | [25.09](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-25-09.html) | 2.9.0a0+50eac81 | 13.0.1.012 | 2.27.7 | 9.13.0.50 | 13.0.2.14 |

- **23.04** 的 CI 使用基于 NGC **22.12** 的内部 `pytest-cov` 镜像，因此首表列的是 22.12 的公开基础组件。**0.4.0** 的默认测试镜像为 23.04，部分测试单独指定了 23.07 或定制 23.10。[23.04 CI](releases/23.04/.gitlab-ci.yml) · [0.4.0 CI](releases/core_v0.4.0/.gitlab-ci.yml)
- **0.15.3** 的包声明要求 `torch>=2.6.0`，同一 tag 的 LTS 配置仍指向自带 PyTorch 2.2 开发版的 24.01。按包声明安装时，dev 基础镜像 25.09 满足该下限。[包声明](releases/core_v0.15.3/pyproject.toml) · [CI 矩阵](releases/core_v0.15.3/.gitlab/stages/01.build.yml)
- **0.19.0、0.19.2** 的 26.06 基础镜像自带 NCCL 2.30.4，dev 构建安装 `libnccl2` 和 `libnccl-dev` 的 `2.30.7-1+cuda13.3` 包。**0.20.0、0.20.1** 的 CI 传入 26.09，覆盖 Dockerfile 的 26.06 默认基础镜像，再把 cuBLAS 和 cuBLASLt 从 13.8.0.4 换为 13.8.1.7，以修复 grouped GEMM 的正确性问题。[0.19 安装脚本](releases/core_v0.19.0/docker/common/install_nccl.sh) · [0.20 CI 矩阵](releases/core_v0.20.1/.gitlab/stages/01.build.yml) · [0.20 dev Dockerfile](releases/core_v0.20.1/docker/Dockerfile.ci.dev)
- **部分镜像元数据与月报列出的版本不同。** 25.05 的 PyTorch 镜像标记 cuDNN 9.10.1.4，CUDA DL 月报列 9.10.1.3。25.11 的镜像标记 NCCL 2.28.8，月报列 2.27.7。26.02 的镜像使用 NCCL 构建标识 `2.29.stable.20260109`，月报列 2.29.2。首表保留镜像原值。可用下列命令只读核对任一基础镜像。[NGC 镜像目录](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch) · [25.05 月报](https://docs.nvidia.com/deeplearning/frameworks/cuda-dl-release-notes/rel-25-05.html) · [25.11 月报](https://docs.nvidia.com/deeplearning/frameworks/cuda-dl-release-notes/rel-25-11.html) · [26.02 月报](https://docs.nvidia.com/deeplearning/frameworks/cuda-dl-release-notes/rel-26-02.html)

```sh
skopeo --override-os linux --override-arch amd64 inspect --config docker://nvcr.io/nvidia/pytorch:26.09-py3 \
  | jq -r '.config.Env[] | select(test("^(PYTORCH|CUDA|NCCL|CUDNN|CUBLAS|TRANSFORMER_ENGINE)_VERSION="))'
```

## 源码安装约束

相同声明合并在一行。早期版本按仓库的 `requirements.txt` 和对应的 `setup.py` 读取。从 0.13.0 起按 `pyproject.toml` 的 `project.dependencies` 与 `requires-python` 读取。`dev`、`lts`、训练和测试使用的额外依赖可在同一份配置中查看。

| 版本范围 | Python 声明 | PyTorch 与其他直接依赖或环境约束 | 依据 |
|---|---|---|---|
| v2.5 | ≥3.6，README 实测 3.8 | `torch`、`numpy`、`pybind11`、`six`、`regex` 未锁版。训练说明另外要求 NVIDIA Apex，实测 PyTorch 1.8 开发版。 | [setup.py](releases/v2.5/setup.py) · [requirements](releases/v2.5/requirements.txt) · [训练说明](releases/v2.5/README.md) |
| 23.04 至 0.8.0 | 未声明下限 | Core 的 requirements 列出 `torch`，未指定版本。早期 Megatron-LM 训练说明另外列出 Apex。 | [23.04 安装脚本](releases/23.04/setup.py) · [0.8.0 requirements](releases/core_r0.8.0/megatron/core/requirements.txt) |
| 0.9.0 | 未声明下限 | Core 的 requirements 列出 `torch` 和 `packaging`，均未指定版本。 | [requirements](releases/core_r0.9.0/megatron/core/requirements.txt) |
| 0.10.0 | 未声明下限 | `PY_ENV` 默认选 24.07。该环境清单锁定 `tensorstore==0.1.45`，在非 macOS 上要求 `nvidia-modelopt[torch]>=0.19.0`。Core 单独列出 `torch`，未指定版本。 | [setup.py](releases/core_r0.10.0/setup.py) · [默认环境](releases/core_r0.10.0/requirements/pytorch:24.07/requirements.txt) · [Core requirements](releases/core_r0.10.0/megatron/core/requirements.txt) |
| 0.11.0 | 未声明下限 | 24.10 默认环境列出 `torch`，排除 `tensorstore` 0.1.46、0.1.72。非 macOS 上要求 `nvidia-modelopt[torch]>=0.19.0`。 | [默认环境](releases/v0.11.0/requirements/pytorch_24.10/requirements.txt) |
| 0.12.0 至 0.12.3 | 未声明下限 | 25.03 默认环境沿用上述 `torch` 和 `tensorstore` 约束，ModelOpt 下限提高到 0.23.2。 | [默认环境](releases/core_v0.12.3/requirements/pytorch_25.03/requirements.txt) |
| 0.13.0、0.13.1 | ≥3.10 | `torch`、`numpy<2.0.0` | [pyproject.toml](releases/core_v0.13.1/pyproject.toml) |
| 0.14.0 | ≥3.10 | `torch`、`numpy<2.0.0`、`packaging` | [pyproject.toml](releases/core_v0.14.0/pyproject.toml) |
| 0.15.0 至 0.15.2 | ≥3.10 | `torch`、`numpy<2.0.0`、`packaging>=24.2` | [pyproject.toml](releases/core_v0.15.2/pyproject.toml) |
| 0.15.3 | ≥3.10 | `torch>=2.6.0`、`numpy<2.0.0`、`packaging>=24.2` | [pyproject.toml](releases/core_v0.15.3/pyproject.toml) |
| 0.16.0、0.16.1 | ≥3.10 | `torch>=2.6.0`、`numpy`、`packaging>=24.2` | [pyproject.toml](releases/core_v0.16.1/pyproject.toml) |
| 0.17.0 至 0.20.1 | ≥3.12 | `torch>=2.6.0`、`numpy`、`packaging>=24.2` | [0.17.0 声明](releases/core_v0.17.0/pyproject.toml) · [0.20.1 声明](releases/core_v0.20.1/pyproject.toml) |

0.12.x 与 0.13.x 的 dev 构建直接从提交编译 TE，表中 `+` 后给出提交缩写。0.14.0 起列出锁文件解析出的 TE 构建。0.20.1 的 `nvidia-cudnn-frontend[cutedsl]==1.29.1` 属于 dev 额外依赖，cuDNN 运行库版本另见 GPU 依赖表。[TE 0.12.x 对应版本文件](https://github.com/NVIDIA/TransformerEngine/blob/bee4649c15a79ffcb9689ca7c0c963f5febaa28a/build_tools/VERSION.txt) · [TE 0.13.x 对应版本文件](https://github.com/NVIDIA/TransformerEngine/blob/8382eed6cccb1eb0602c96afc1cfbc707468257f/build_tools/VERSION.txt) · [0.20.1 dev 配置](releases/core_v0.20.1/pyproject.toml)

## 逐版新增特性与修复

比较顺序与依赖表一致，按仓库收录的相邻版本号对照。补丁可能晚于后续主线发布。0.18.2 和 0.19.2 分别对照本仓库的 0.18.0 和 0.19.0。每行选取影响模型、训练、推理或兼容性的主要变化。链接可查看发布说明或两个 tag 间的完整差异。

| Megatron tag | 上一快照 | 新增特性或修复 | 依据 |
|---|---|---|---|
| `v2.5` | — | 收录起点。提供 GPT、BERT、T5 预训练。可组合张量并行、流水线并行与数据并行，并使用交错流水线调度。 | [快照说明](releases/v2.5/README.md) |
| `23.04` | `v2.5` | 引入可独立安装的 `megatron.core`，抽出张量与流水线并行组件。加入序列并行、选择性激活重计算、分布式优化器、FlashAttention 选项和 RETRO 预训练入口。 | [快照说明](releases/23.04/README.md) · [Core 包](releases/23.04/setup.py) |
| `core_v0.4.0` | `23.04` | Core 增加 BERT、T5、RETRO 模型，以及 GPT 的混合专家（MoE）、上下文并行、面向模型并行的 DDP 和混合数据集。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.4.0) |
| `core_v0.5.0` | `core_v0.4.0` | MoE 支持不丢 token 的 Top-K 路由、GroupedGEMM 和分布式检查点。增加 CPU 激活卸载、RoPE/SwiGLU 融合，以及通过 TE 使用的滑动窗口注意力。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.5.0) |
| `core_v0.6.0` | `core_v0.5.0` | 新增基于 all-to-all 的 MoE token 分发器，支持梯度归约、参数收集与计算重叠。分布式检查点接入 PyTorch 原生后端，TensorRT-LLM 导出接入 Model Optimizer 的训练后量化。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.6.0) |
| `core_v0.7.0` | `core_v0.6.0` | MoE 可按容量丢弃 token。分布式检查点支持异步保存，并扩展到 RETRO。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.7.0) |
| `core_r0.8.0` | `core_v0.7.0` | 加入 LLaVA 视觉语言模型训练和多模态推理示例，支持 Mamba-2 及其与注意力、MLP 混合的模型。MoE 支持上下文并行，GroupedGEMM 专家支持分布式检查点。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_r0.8.0) |
| `core_r0.9.0` | `core_r0.8.0` | 支持流水线首尾阶段分配较少层、GPT 逐层 CUDA Graph、T5/LLaVA 流水线并行。MoE 加入 FP8、共享专家及从稠密模型转换为 MoE 的运行时 upcycling。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_r0.9.0) |
| `core_r0.10.0` | `core_r0.9.0` | 引入多头潜在注意力（MLA）。MoE 的注意力层与专家层可采用不同的并行布局（Parallel Folding），GroupedMLP 支持 FP8。新增 NVLM 训练与评估。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_r0.10.0) |
| `v0.11.0` | `core_r0.10.0` | 支持 DeepSeek-V3 微调，加入无辅助损失的负载均衡、节点或设备受限路由及 MLA 张量并行。另支持跨数据中心训练与优化器 CPU 卸载。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/v0.11.0) · [变更记录](releases/core_v0.15.3/CHANGELOG.md) |
| `core_v0.12.0` | `v0.11.0` | MoE 接入 DeepEP、CUDA Graph 和多 token 预测（MTP），可选 FP32/FP64 路由。推理加入连续批处理与分块 KV 缓存，训练可选择 FP8 配方并保留首尾层 BF16。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.12.0) |
| `core_v0.12.1` | `core_v0.12.0` | 融合 RoPE 在 TE ≥2.2.0.dev0 时支持交错旋转布局。MoE 分发可连同路由概率一起做融合置换，并对 `alltoall_seq` 的不兼容配置提前报错。 | [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.12.0...core_v0.12.1) · [源码](releases/core_v0.12.1/megatron/core/transformer/transformer_config.py) |
| `core_v0.12.2` | `core_v0.12.1` | 收紧 MoE 层频率自定义表达式的输入校验。文本生成 CLI 改用字面量解析用户输入的生成长度。 | [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.12.1...core_v0.12.2) · [源码](releases/core_v0.12.2/megatron/training/arguments.py) |
| `core_v0.12.3` | `core_v0.12.2` | 异步文件系统检查点用 `spawn` 创建结果队列的管理进程。训练参数 YAML 改用 `safe_load`。 | [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.12.2...core_v0.12.3) · [源码](releases/core_v0.12.3/megatron/core/dist_checkpointing/strategies/filesystem_async.py) |
| `core_v0.13.0` | `core_v0.12.3` | 支持自定义非对称虚拟流水线布局、MoE 混合分片数据并行，以及 DeepSeek-V3 的专家并行与自定义 FSDP 联用。MTP 支持 FP8，激活可按模块选择性重计算。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.13.0) |
| `core_v0.13.1` | `core_v0.13.0` | 在 0.13 分支将训练参数 YAML 切换到 `safe_load`，并启用 Ruff `S506` 检查以发现不安全的 YAML 加载调用。 | [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.13.0...core_v0.13.1) · [源码](releases/core_v0.13.1/megatron/training/yaml_arguments.py) |
| `core_v0.14.0` | `core_v0.13.1` | 动态推理引擎支持异步调用和多种 batch size 的 CUDA Graph。专家并行可将 all-to-all 与计算重叠，MTP 支持上下文并行和重计算。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.14.0) |
| `core_v0.15.0` | `core_v0.14.0` | 加入 Muon 及其分布式优化器支持。融合 QKV 预处理可复用 RoPE 缓存。MoE Flex 分发器接入 HybridEP，新增 GPT-OSS 的 YaRN 支持和 Qwen3-Next 参数。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.15.0) · [变更记录](releases/core_v0.15.3/CHANGELOG.md) |
| `core_v0.15.1` | `core_v0.15.0` | 上游标记为已撤回（yanked）。与 0.15.0 对照，快照只更新 Core 和 Megatron-FSDP 的包版本号。 | [变更记录](releases/core_v0.15.3/CHANGELOG.md) · [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.15.0...core_v0.15.1) |
| `core_v0.15.2` | `core_v0.15.1` | 修复 Megatron-FSDP 的 DeviceMesh 兼容性，支持自动创建默认 mesh，并从 `fully_shard_optimizer()` 接口移除 `model` 参数。 | [变更记录](releases/core_v0.15.3/CHANGELOG.md) · [快照差异](https://github.com/NVIDIA/Megatron-LM/compare/core_v0.15.1...core_v0.15.2) |
| `core_v0.15.3` | `core_v0.15.2` | 安全维护版。量化配方 YAML 切换为 `SafeLoader`，Core 包的 PyTorch 下限提高至 2.6.0。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.15.3) · [量化配置](releases/core_v0.15.3/megatron/core/quantization/quant_config.py) |
| `core_v0.16.0` | `core_v0.15.3` | 支持 DeepSeek V3.2，MTP 层可独占流水线阶段并使用打包序列。MoE 可回放路由决策以调试或训练 RL 模型，专家通信重叠可使用局部 CUDA Graph。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.16.0) |
| `core_v0.16.1` | `core_v0.16.0` | 修复 Mamba 层数不均时的流水线划分。持久化异步检查点工作进程在循环中显式触发垃圾回收。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.16.1) |
| `core_v0.17.0` | `core_v0.16.1` | 加入吸收式 MLA 与融合投影、μP 参数化和 Lion 优化器。推理支持 KV 前缀缓存及基于 MTP 的推测解码，MIMO 多模块训练支持异构并行。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.17.0) |
| `core_v0.17.1` | `core_v0.17.0` | DDP 支持原生 NVFP4 权重。回移 HybridEP 置换融合与 NVRx 异步检查点兼容修复，新增检查点完整性校验，前缀缓存改用 SHA-256。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.17.1) |
| `core_v0.18.0` | `core_v0.17.1` | Megatron-FSDP 支持专家 all-to-all 与计算重叠，MLP 训练支持分块，Gated DeltaNet 支持打包序列。MoE 推理增加 AllGatherV 分发器与 vLLM grouped GEMM 后端。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.18.0) |
| `core_v0.18.2` | `core_v0.18.0` | 因稳定性问题在训练参数检查中禁用 TE 交叉熵融合。CI 从源码编译 FlashMLA，并更新 TE 2.16 的补丁提交。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.18.2) |
| `core_v0.19.0` | `core_v0.18.2` | 新一代 `HybridModel` 可直接载入 `GPTModel` 检查点并支持 MLA。DeepSeek 稀疏注意力扩展到上下文并行和打包序列。MoE 增加基于分位数的负载均衡路由。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.19.0) |
| `core_v0.19.2` | `core_v0.19.0` | 1F1B 流水线的 all-to-all 通信重叠支持 FP4，TE 从 2.17 系列升级至 2.18。服务端收紧对请求自带聊天模板的处理。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.19.2) |
| `core_v0.20.0` | `core_v0.19.2` | `HybridModel` 完整支持 DeepSeek-V4。MoE 加入实验性 DeepEP v2 和 NCCL EP 的 MXFP8 通信。Megatron-FSDP v2 增加分布式检查点，推理支持用 NCCL/NIXL 在 prefill 与 decode 间传递 KV 缓存。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.20.0) |
| `core_v0.20.1` | `core_v0.20.0` | 接入 Mixture-of-Kittens MoE 后端，TE 升级到 2.21，回移 Megatron-FSDP v2 的专家并行检查点支持，以及融合 MLA KV RoPE 的 MXFP8 量化。 | [发布说明](https://github.com/NVIDIA/Megatron-LM/releases/tag/core_v0.20.1) |
