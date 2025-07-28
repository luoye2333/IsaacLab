# isaaclab安装
```bash
# ubuntu20.04 gcc版本不够(glibc>2.34) 可能下载不了报错
# 查看gcc版本 
ldd --version

# 设置pip和conda镜像
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
pip config list

conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --show channels

# 创建conda环境
conda create -n env_isaaclab python=3.10
conda activate env_isaaclab

# 安装isaacsim
pip install 'isaacsim[all,extscache]==4.5.0' --extra-index-url https://pypi.nvidia.com

# import torch如果报错 可能是cuda版本和torch不匹配
pip install torch torchvision torchaudio --index-url https://mirrors.aliyun.com/pytorch-wheels/cu118

# 验证isaacsim安装
isaacsim

# 安装isaaclab(不要用pip安装 相对最新的库有延迟)
# pip install isaaclab[isaacsim,all]==2.1.0 --extra-index-url https://pypi.nvidia.com
git clone https://github.com/isaac-sim/IsaacLab.git

# robomimic库clone很慢 手动安装
git clone https://ghproxy.net/https://github.com/ARISE-Initiative/robomimic.git
pip install .
# 把source/isaaclab_mimic/setup.py里面的robomimic注释掉

# 运行lab官方的安装脚本
# 这个脚本会强制卸载已有的torch重新安装torch=2.7.0 cuda=12.8 这应该是个bug 已经提了issue应该会很快解决 目前先注释isaaclab.sh的281~295行就行
./isaaclab.sh --install # or "./isaaclab.sh -i"


# 验证安装
./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/train.py --task=Isaac-Ant-v0 --headless
```

# isaaclabExt安装

```bash
git clone https://github.com/isaac-sim/IsaacLabExtensionTemplate.git

python -m pip install -e source/ext_template

#验证安装
python scripts/rsl_rl/train.py --task=Template-Isaac-Velocity-Rough-Anymal-D-v0 --num_envs=32 --headless
```