# Reverse Image Search Based on Milvus （v2.0）

This demo is an updated version of the original image search system, replacing the original image feature extraction model VGG with Resnet 50, adding the target detection function for images, and then building a reverse image search system in combination with Milvus.

The system architecture is shown below.

<img src="pic\demo1.png" alt="demo1" style="zoom:40%;" />

### Environment requirements

The following tables show recommended configurations for reverse image search. These configurations haven been tested.


| Component     | Recommended Configuration                                                    |
| -------- | ------------------------------------------------------------ |
| CPU      | Intel(R) Core(TM) i7-7700K CPU @ 4.20GHz                     |
| Memory   | 32GB                                                         |
| OS       | Ubuntu 18.04                                                 |
| Software | Milvus 0.10.5<br />pic_search_webclient  0.2.0<br / |

### Data source

This demo uses the PASCAL VOC image set, which contains 17125 images with 20 categories: human; animals (birds, cats, cows, dogs, horses, sheep); transportation (planes, bikes,boats, buses, cars, motorcycles, trains); household (bottles, chairs, tables, pot plants, sofas, TVs)

Dataset size: ~ 2 GB.

Download location: https://pan.baidu.com/s/1MjACqsGiLo3oiTMcxodtdA extraction code: v78m

> Note: You can also use other images for testing. This system supports the following formats: .jpg and .png.

### How to deploy the system

### GPU method

#### 1. Run Milvus Docker

This demo uses Milvus 0.10.5. Refer to the [Install Milvus](https://www.milvus.io/cn/docs/v0.10.5/milvus_docker-gpu.md) for how to run Milvus docker.

#### **2.Install the Python packages you need**

```
cd /image_search/webserver
pip install -r requirements.txt

```

#### 3.start query service

```
cd  /image_search/webserver/src
python app.py
```

#### 4. Run pic-search-webclient docker

```bash
$ docker run --name zilliz_search_images_demo_web -d --rm -p 8001:80 \
-e API_URL=http://${WEBSERVER_IP}:5000 \
milvusbootcamp/pic-search-webclient:0.2.0
```

In the previous command, WEBSERVER_IP specifies the server IP address that runs pic-search-webserver docker.

### How to perform reverse image search

After deployment, enter ` ${WEBCLIENT_IP}:8001` in the browser to open the interface for reverse image search. **WEBCLIENT_IP** specifies the server IP address that runs pic-search-webclient docker.

<img src="pic/web4.png" width = "650" height = "500" alt="arch" align=center />

Enter the path to the images folder, e.g. /data/images. click Load to load the images. The following screenshot shows the loading process.

<img src="pic/web0.png" width = "650" height = "500" alt="arch" align=center  />

> Note: After clicking the load button, the system needs to wait for a while to respond. Please do not click again

The loading process may take several minutes. The following screenshot shows the interface with images loaded.

<img src="pic\web3 .png" width = "650" height = "500" />

Select an image to search.

<img src="pic/web5.png"  width = "650" height = "500" />

Tested with the recommended configuration, the system can complete a reverse image search in a few seconds. To load images from other directories, specify the path in the text box.

