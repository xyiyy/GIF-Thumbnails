# GIF-Thumbnails

This repo is the official implementation of the paper of [GIF-Thumbnails](https://www.aaai.org/AAAI21Papers/AAAI-1201.XuY.pdf): **GIF Thumbnails: Attract More Clicks to Your Videos**(AAAI-21).

<img src="./imgs/Cover1.jpg" width="300" /> <img src="./imgs/Gif1.gif" width="300" />

## Environment
* NVIDIA P40
* Python 3.7
* Pytorch 1.4

## DataSet
### Video
Videos are provided in the json **annotated.json** and **unannotated.json**. 
For annotated data, json is organized as:
```
{
    $video_hash_key: {
        "gifs": {
            $gif_id1: [idx1, idx2, idx3], ...
            $gif_idn: [idx1, idx2, idx3],
        },
        "video_url": $url,
        "height": $height,
        "width": $width,
        "fps": $fps,
        "frames": $frames,
    }, ...
}
```
For unannotated data, videos are listed as:
```
{
    $video_hash_key: {
        "seconds": $seconds,
        "video_url": $url
    }
}
```

Download videos by [you-get](https://github.com/soimort/you-get)
```
you-get --format=flv720 https://www.bilibili.com/video/av18182135 -O 18182135.flv
```
Then we process the video to fps=16 and new_height=240 with ffmpeg
```
ffmpeg -i $InputVideo -r 16 -vf scale=$new_width:$new_height -qscale 0 $OutputVideo
```
where $new\_width=width \times \frac{new\_height}{height}$

**Considering that some videos has been removed and are not available on bilibili now, we provide the feature of these videos extracted by 3D-ResNet-50. 
Features are released on the [BaiduDisk](https://pan.baidu.com/s/1o4WjdHLXFb9orle4l3UwMw) with code `r9p1`.**


### Time-sync Comments
For time-sync comments, we only release the number of comments in each second. 
```
{
    $video_hash_key: [cnt_1, cnt_2, ..., cnt_n],
    ...
}
```
Time-sync comments and video share the same video_hash_key, and $n$ is the number of frames

# Citation
If you find this project is useful for your research, please cite:
```
@inproceedings{xu2021gif,
  title={GIF Thumbnails: Attract More Clicks to Your Videos},
  author={Xu, Yi and Bai, Fan and Shi, Yingxuan and Chen, Qiuyu and Gao, Longwen and Tian, Kai and Zhou, Shuigeng and Sun, Huyang},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence},
  volume={35},
  number={4},
  pages={3074--3082},
  year={2021}
}
```
