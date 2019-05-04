Get the preprocessed data (you can also preprocess the semantic data from raw data in the directory dataset/preprocessing) :
- Scannet : https://onedrive.live.com/?authkey=%21AHEO5Ik8Hn4Ue2Y&cid=423FEBB4168FD396&id=423FEBB4168FD396%21136&parId=423FEBB4168FD396%21134&action=locate
- Semantic : https://drive.google.com/file/d/1-l2h3yh1xBAzR2JhqPz-YIzM4vtEOf4W/view?usp=sharing

Compiling the C++ parts if you want to preprocess the data or to calculate results on the raw data can result in the following error : "/usr/bin/ld: cannot find -lvtkproj4", but you can overcome this difficulty by using this trick : ln -s /usr/lib/x86_64-linux-gnu/libvtkCommonCore-6.2.so /usr/lib/libvtkproj4.so (see https://github.com/PointCloudLibrary/pcl/issues/1594 for details).


下载原始数据 , go into dataset/ directory and use the command:
./downloadAndExtractSem8.sh


处理原始数据并选择合适的voxel_size, go into the preprocessing directory and use the command:
./preprocess.sh ../dataset/raw_semantic_data ../dataset/semantic_data 'voxel_size'
(with the voxel_size you want, in m. default is 0.05)

For training, use python train.py --config=your_config --log=your_logs
Both scannet and semantic_8 should be trainable.

For interpolating results, first use predict.py --cloud=true --n=100 --ckpt=your_ckpt --dataset=semantic --set=test for example. Files will be created in visu/semantic_test/full_scenes_predictions and will contain predictions on sparse point clouds.


----------------------应为获得预测结果,但如何可视化？


The actual interpolation is done in interpolation directory with the command:
./interpolate path/to/raw/data visu/semantic_test/full_scenes_predictions /path/to/where/to/put/results 'voxel_size'
(with the voxel_size you want, in m. default is 0.1)


----------------------暂不理解,插值？
