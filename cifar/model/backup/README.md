<font size=4><b>Reproduced ResNet on CIFAR-10 and CIFAR-100 dataset.</b></font>

contact: panyx0718 (xpan@google.com)

<b>Dataset:</b>

https://www.cs.toronto.edu/~kriz/cifar.html

<b>Related papers:</b>

Identity Mappings in Deep Residual Networks

https://arxiv.org/pdf/1603.05027v2.pdf

Deep Residual Learning for Image Recognition

https://arxiv.org/pdf/1512.03385v1.pdf

Wide Residual Networks

https://arxiv.org/pdf/1605.07146v1.pdf

<b>Settings:</b>

* Random split 50k training set into 45k/5k train/eval split.
* Pad to 36x36 and random crop. Horizontal flip. Per-image whitenting. 
* Momentum optimizer 0.9.
* Learning rate schedule: 0.1 (40k), 0.01 (60k), 0.001 (>60k).
* L2 weight decay: 0.002.
* Batch size: 128. (28-10 wide and 1001 layer bottleneck use 64)

<b>Results:</b>

<left>
![Precisions](g3doc/cifar_resnet.gif)
</left>
<left>
![Precisions Legends](g3doc/cifar_resnet_legends.gif)
</left>


CIFAR-10 Model|Best Precision|Steps
--------------|--------------|------
32 layer|92.5%|~80k
110 layer|93.6%|~80k
164 layer bottleneck|94.5%|~80k
1001 layer bottleneck|94.9%|~80k
28-10 wide|95%|~90k

CIFAR-100 Model|Best Precision|Steps
---------------|--------------|-----
32 layer|68.1%|~45k
110 layer|71.3%|~60k
164 layer bottleneck|75.7%|~50k
1001 layer bottleneck|78.2%|~70k
28-10 wide|78.3%|~70k

<b>Prerequisite:</b>

1. Install TensorFlow, Bazel.

2. Download CIFAR-10/CIFAR-100 dataset.

```shell
curl -o cifar-10-binary.tar.gz https://www.cs.toronto.edu/~kriz/cifar-10-binary.tar.gz
curl -o cifar-100-binary.tar.gz https://www.cs.toronto.edu/~kriz/cifar-100-binary.tar.gz
```

<b>How to run:</b>

```shell
# cd to the your workspace.
# It contains an empty WORKSPACE file, resnet codes and cifar10 dataset.
# Note: User can split 5k from train set for eval set.
ls -R
  .:
  cifar10  resnet  WORKSPACE

  ./cifar10:
  data_batch_1.bin  data_batch_2.bin  data_batch_3.bin  data_batch_4.bin
  data_batch_5.bin  test_batch.bin

  ./resnet:
  BUILD  cifar_input.py  g3doc  README.md  resnet_main.py  resnet_model.py

# Build everything for GPU.
bazel build -c opt --config=cuda resnet/...

# Train the model.
bazel-bin/resnet/resnet_main --train_data_path=cifar10/data_batch* \
                             --log_root=/tmp/resnet_model \
                             --train_dir=/tmp/resnet_model/train \
                             --dataset='cifar10' \
                             --num_gpus=1

# Evaluate the model.
# Avoid running on the same GPU as the training job at the same time,
# otherwise, you might run out of memory.
bazel-bin/resnet/resnet_main --eval_data_path=cifar10/test_batch.bin \
                             --log_root=/tmp/resnet_model \
                             --eval_dir=/tmp/resnet_model/test \
                             --mode=eval \
                             --dataset='cifar10' \
                             --num_gpus=0
```






python cori-tuning-hdf5.py --n_parallel_jobs=1 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w1_async_b4_prof' --n_workers=1 --n_param_servers=6 --time_out_minutes=2 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1

python cori-tuning-hdf5.py --n_parallel_jobs=2 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w2_async_b4_prof' --n_workers=2 --n_param_servers=6 --time_out_minutes=2 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2

python cori-tuning-hdf5.py --n_parallel_jobs=3 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w4_async_b4_prof' --n_workers=4 --n_param_servers=6 --time_out_minutes=2 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,4

python cori-tuning-hdf5.py --n_parallel_jobs=3 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w8_async_b4_prof' --n_workers=8 --n_param_servers=6 --time_out_minutes=3 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,8


python cori-tuning-hdf5.py --n_parallel_jobs=4 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w16_async_b4_prof' --n_workers=16 --n_param_servers=6 --time_out_minutes=8 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,8,16


python cori-tuning-hdf5.py --n_parallel_jobs=5 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w32_async_b4_prof' --n_workers=32 --n_param_servers=6 --time_out_minutes=15 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,8,16,32


python cori-tuning-hdf5.py --n_parallel_jobs=5 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w64_async_b4_prof' --n_workers=64 --n_param_servers=6 --time_out_minutes=15 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,8,16,64

python cori-tuning-hdf5.py --n_parallel_jobs=5 --async_branch=1 --async_caffe_root='/project/projectdirs/dasrepo/zjian/caffe_git_async_rebase_mult_proc_server_prof/caffe-1' --base_dir='/project/projectdirs/dasrepo/zjian/Climate-scripts' --experiment_name='w128_async_b4_prof' --n_workers=128 --n_param_servers=6 --time_out_minutes=25 --use_group_batch=0 --worker_batch_size=4 --hdf5_path='/global/cscratch1/sd/zjian/HEP_data' --all_n_groups=1,2,8,16,128

