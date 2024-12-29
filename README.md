# esmFold

部署了esmfold几天，要吐了，总结了要点
首先准备environment.yaml文件,进行下面的安装
'''
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

'''
准备好后运行`conda env create -f environment.yml`
随后准备requirement.txt文件
'''
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
'''
准备好后运行`pip install -r requirement.txt`

大概率会出现gcc和g++的问题，解决方法见
'''
conda install -c moussi gcc_impl_linux-64=7.3.0
conda install -c moussi gxx_impl_linux-64=7.3.0
cd /home/line2/anaconda3/envs/esmfold_env/bin
##链接到gcc和gxx(进入自己的bin看叫gcc和gxx什么名字)
ln -s ./x86_64-conda_cos6-linux-gnu-gcc ./gcc
ln -s ./x86_64-conda_cos6-linux-gnu-g++ ./g++
'''

上述方案参考：
https://github.com/aqlaboratory/openfold/issues/500
https://blog.csdn.net/weixin_52004233/article/details/140044303?ops_request_misc=%257B%2522request%255Fid%2522%253A%252277daf44805ccf6aa914cad152db8dc98%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=77daf44805ccf6aa914cad152db8dc98&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-140044303-null-null.142^v100^pc_search_result_base2&utm_term=openfold%E4%B8%8B%E8%BD%BD&spm=1018.2226.3001.4187


