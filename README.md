# JavaScript

脚本使用：点击打开脚本文件，在右侧找到raw按钮并点击，然后复制打开的网页地址，添加至小奶猫++即可。

制作脚本说明：

```javascript

//以下三个方法必须存在且名称不可更改，其中涉及到的字典中的key的名字也是固定的，否则无法解析

//封面信息（key、方法名不可更改， "source":"JS"不可缺少）
function coverInfo() {
    var name = "花姬2";
    var imageURL = "http://cdn.63a0.com/Uploads/Advertisement/20200717_152741_15949708617555_1660.jpg";
    var online = "100";
    return { "name": name, "logo": imageURL, "source":"JS", "quantity":online };
}

//房间列表（key、方法名不可更改）
function videoListInfo() {
    var url = "https://cdn.63a0.com/index.php/Api/LiveApi/getPlatformlist";
    var method = "POST";
    var param = { "id": "107" };
    var header = {};
    return { "url": url, "method": method, "param": param, "header": header };
}

//处理网络数据，统一格式（key、方法名不可更改）
function handleData(dic) {
    //dic 为字典(房间列表url返回的数据)，需经过处理，最终如下,key的名称必须如下所示
    // {
    //     "data": [
    //         {
    //             "name": "TG@iCodess",
    //             "title": "TG@iCodess",
    //             "city": "TG@iCodess",
    //             "headimage": "https://downaoligie.oss-cn-qingdao.aliyuncs.com/65.jpg",
    //             "cover": "https://downaoligie.oss-cn-qingdao.aliyuncs.com/65.jpg",
    //             "video": "rtmp://tpull.amghkwy.cn/live/9185723_1598444341?txSecret=cf2a19ff267b69c798f7f8bb0e95d574&txTime=5F45AA75",
    //             "Popularity": "666666",
    //             "id": "999999"
    //         },
    //         ...
    // }

    var dataArr = dic["data"];
    var formatArr = new Array();
    for (let i = 0; i < dataArr.length; i++) {
        let subDic = dataArr[i];
        var formatDic = {
            "name": subDic["title"],
            "Popularity": subDic["watch_number"],
            "video": subDic["address"],
            "cover": subDic["header"],
            "id": subDic["room_id"]
        };
        formatArr.push(formatDic);
    }

    return { "data": formatArr };
}
```
