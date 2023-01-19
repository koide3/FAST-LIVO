# FAST_LIVO

Original repository: https://github.com/hku-mars/FAST-LIVO

## Build
```bash
cd FAST_LIVO/docker
./build.sh
```

## Run

[hku1.bag](https://connecthkuhk-my.sharepoint.com/:f:/g/personal/zhengcr_connect_hku_hk/Esiqlmaql0dPreuOhiHlXl4Bqu5RRRIViK1EyuR4h1_n4w?e=fZdVn0)

### On docker image
```bash
cd FAST_LIVO/docker
./run.sh

roslaunch fast_livo mapping_avia.launch
```

### On host

```bash
cd FAST_LIVO/rviz_cfg
rviz -d loam_livox.rviz
```

```bash
rosbag play hku1.bag
```

![ezgif com-gif-maker](https://user-images.githubusercontent.com/31344317/213341608-d5443ae7-a151-4731-ac34-959dc5c4654b.gif)
