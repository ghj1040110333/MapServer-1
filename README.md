# 这里是MapServer的后端源码

## 前端源码在这里：https://github.com/Icemap/MapServer-Front

## 这是一个在需要本地化部署地图服务时，快速建立本地瓦片地图服务的小工具。

## 比如你部署服务的位置不能访问外网，但是你的前端又需要一个地图控件。或者你需要对地图瓦片进行处理，需要地图色调变成“五彩斑斓的黑色”，美工让你下载切片。那么这个工具可以帮你快速建立这样的瓦片地图服务。

## 这个后端小工具使用Java、Spring Boot编写。

## 基本思路为：
> - 将传入的经纬度形式的矩形参数，转换成Web墨卡托形式的矩形参数（CoodUtils.java）;
> - 通过转换后的Web墨卡托参数形式的矩形，以及传入的地图类型、地图等级，计算出需下载的切片URL（InitUtils.java）;
> - 使用URL得到地图瓦片（HttpUtils.java）;
> - 保存至相应位置（FileUtils.java）;
> - 请求时返回相应位置的文件（ServerController.java）;

--------

## 支持地图类型为：
> - Google卫星
> - Google矢量
> - Google地形
> - 高德卫星
> - 高德矢量
> - 高德标签层
> - 天地图卫星
> - 天地图矢量
> - 天地图标签层
> - PS：多种类型的瓦片类型可以同时存在。
> - PSS：瓦片保存位置为 ./map。

--------

## 坐标系：
> - Google与高德使用的大地坐标系为GCJ02，是加过偏的，使用时需要注意转经纬度。
> - 天地图使用的大地坐标系为WGS84，是不加偏的，国家队待遇就是不一样=。=

--------

## API简述：

#### 1. 初始化地图(下载切片)
> - /init/initMap POST, 参数为：
> - left : 类型：double, 单位：经纬度, 含义：请求瓦片的左边界
> - right : 类型：double, 单位：经纬度, 含义：请求瓦片的右边界
> - top : 类型：double, 单位：经纬度, 含义：请求瓦片的上边界
> - bottom : 类型：double, 单位：经纬度, 含义：请求瓦片的下边界
> - type : 类型：string, 单位：瓦片类型, 含义：请求瓦片的类型，说明见瓦片类型参数说明
> - level : 类型：int, 单位：瓦片等级, 含义：请求瓦片的等级，说明见瓦片等级参数说明

#### 2. 获取拥有的地图类型、等级、范围
> - /server/config GET, 参数为空

#### 3. 地图服务
> - /server/map/{type}/{x}/{y}/{z} GET, 参数为URL参数，放在请求的路径中:
> - type : 类型：string, 单位：瓦片类型, 含义：请求瓦片的类型，说明见瓦片类型参数说明
> - x : 类型：int, 单位：/, 含义：标准TMS(瓦片地图服务)的x参数
> - y : 类型：int, 单位：/, 含义：标准TMS(瓦片地图服务)的y参数
> - z : 类型：int, 单位：/, 含义：标准TMS(瓦片地图服务)的z参数

## 其余描述：
> -  见前端Q&A页面。
