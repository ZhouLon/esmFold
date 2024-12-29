# ESMFold 部署总结

经过几天的努力部署 ESMFold，总结了一些关键步骤和注意事项，供大家参考。

---

## 环境配置

### 1. 准备 `environment.yaml`
以下是 `environment.yaml` 的内容，用于创建 Conda 环境：
```yaml
name: esmfold
channels:
 - conda-forge
 - bioconda
 - pytorch
dependencies:
 - conda-forge::python=3.7
 - conda-forge::setuptools=59.5.0
 - conda-forge::pip
 - conda-forge::openmm=7.5.1
 - conda-forge::pdbfixer
 - conda-forge::cudatoolkit==11.3.*
 - conda-forge::cudatoolkit-dev==11.3.*
 - conda-forge::einops==0.6.1
 - conda-forge::fairscale
 - conda-forge::omegaconf
 - conda-forge::hydra-core
 - conda-forge::pandas
 - conda-forge::pytest
 - bioconda::hmmer==3.3.2
 - bioconda::hhsuite==3.3.0
 - bioconda::kalign2==2.04
 - pytorch::pytorch=1.12.*
```

运行以下命令创建 Conda 环境：
```conda env create -f environment.yml```

### 2. 准备 `requirement.txt`
以下是 `requirement.txt` 文件的内容，用于安装 Python 依赖：
```
biopython==1.79
deepspeed==0.5.9
dm-tree==0.1.6
ml-collections==0.1.0
numpy==1.21.2
PyYAML==5.4.1
requests==2.26.0
scipy==1.7.1
tqdm==4.62.2
typing-extensions==3.10.0.2
pytorch_lightning==1.5.10
wandb==0.12.21
biotite==0.39.0
joblib
```

运行以下命令安装 Python 包：
```pip install -r requirement.txt```
### 3. 安装esm和openfold
按顺序执行即可
```
pip install fair-esm           # Latest release
pip install git+https://github.com/facebookresearch/esm.git  # Main branch
pip install "fair-esm[esmfold]"
# OpenFold and its dependencies
pip install 'dllogger @ git+https://github.com/NVIDIA/dllogger.git'
pip install 'openfold @ git+https://github.com/aqlaboratory/openfold.git@4b41059694619831a7db195b7e0988fc4ff3a307'
```
### 4. Tips (GCC 和 G++ 问题的解决方案)

在安装过程中，大概率会出现 gcc 和 g++ 版本不兼容的问题，可以按以下步骤解决：
用 Conda 安装指定版本的 gcc 和 g++：
```
conda install -c moussi gcc_impl_linux-64=7.3.0
conda install -c moussi gxx_impl_linux-64=7.3.0
```
进入 Conda 环境的 bin 目录，并创建符号链接：
```
cd /home/line2/anaconda3/envs/esmfold_env/bin
ln -s ./x86_64-conda_cos6-linux-gnu-gcc ./gcc
ln -s ./x86_64-conda_cos6-linux-gnu-g++ ./g++
```
### 参考资料

[OpenFold GitHub Issues #500](https://github.com/aqlaboratory/openfold/issues/500)<br>
[CSDN 博客：OpenFold 下载与配置](https://blog.csdn.net/weixin_52004233/article/details/140044303?ops_request_misc=%257B%2522request%255Fid%2522%253A%252277daf44805ccf6aa914cad152db8dc98%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=77daf44805ccf6aa914cad152db8dc98&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-140044303-null-null.142^v100^pc_search_result_base2&utm_term=openfold%E4%B8%8B%E8%BD%BD&spm=1018.2226.3001.4187)













