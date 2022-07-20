# LoliSuki Api

## 简介
- 一个与[Lolicon Api](https://api.lolicon.app) 类似的api，参考了它的参数和返回格式
- 在[Lolicon Api](https://api.lolicon.app/) 基础上增加了level参数，用于区别图片的涩气程度
- 所有图片均由作者空闲时从pixiv上收集，并非来源于其他色图api


## 调用方式
### Get
```
https://lolisuki.cc/api/setu/v1
```
或者
### POST 
```
https://lolisuki.cc/api/setu/v1
```
```json
{
  "r18": 0,
  "num": 1,
  "proxy": "i.pixiv.re",
  "level":"0-3",
  "full":1,
  "tag": [
    "萝莉|少女",
    "白丝|黑丝"
  ]
}
```

## 参数说明
| 参数名       |  数据类型  |     默认值     |                                    说明                                     |
| ------------ | :--------: | :------------: | -------------------------------------------------------------------------- |
| `r18`        |   `int`    |      `0`       | 作品中是否包含R-18标签，`0`为不包含，`1`为包含，`2`为混合                   |
| `num`        |   `int`    |      `1`       | 返回的结果数量，范围为1~5                                                  |
| `uid`        |  `int[]`   |                | 返回指定uid作者的作品，最多5个                                              |
| `tag`        | `string[]` |                | 返回匹配指定标签的作品，[详见下文](#tag)                                    |
| `proxy`      |  `string`  | `i.pixiv.cat`  | 设置图片地址所使用的在线反代服务                                            |
| `level`      |  `string`  |      `0`       | 指定图片的涩气级别，[详见下文](#level)                                      |
| `full`       |   `int`    |      `0`       | 匹配Tag的方式，`0`为部分一致，`1`为完全一致                                 |

## tag
Get方式请求时，Tag参数可以通过`&`符号连接多个
```
https://lolisuki.cc/api/setu/v1?tag=萝莉&tag=白丝
```
Tag之间用`|`符号隔开时，代表只需要匹配其中任意一个，假如：我需要查找萝莉或者少女的白丝或者黑丝图
```
Get https://lolisuki.cc/api/setu/v1?tag=萝莉|少女&tag=白丝|黑丝
```
或者
```
Post https://lolisuki.cc/api/setu/v1
```
```json
{
  "tag": [
    "萝莉|少女",
    "白丝|黑丝"
  ]
}
```


## level
这是一个根据个人xp整理出来的参数，代表本人认为一张涩图的涉秦程度
- 0：画的不错，很可爱，或者根本一点都不涩
- 1：有点涩
- 2：涩
- 3：很涩
- 4：非常涩但是还不属于R-18，属于从涩图过渡到色图之间的级别
- 5：R18
- 6：R18+多人运动
- 例：如果想要查询level0-level6的作品，参数值可以填`0-6`
- 例：如果只想查询level3的作品，参数值可以填`3`

## 响应
| 字段名	  | 数据类型 | 说明                             |
| ------- | :------: | -------------------------------- |
| `code`  | `int`    | 状态码，`0`表示成功，其他均为失败 |
| `error` | `string` | 错误信息                         |
| `data`  | `setu[]` | 色图数组                         |

### `setu`

| 字段名        |  数据类型   | 说明                                                  |
| ------------- | :--------: | ----------------------------------------------------- |
| `pid`         |   `int`    | 作品 pid                                              |
| `p`           |   `int`    | 作品所在页                                            |
| `total`       |   `int`    | 作品包含的图片数量                                    |
| `uid`         |   `int`    | 作者 uid                                              |
| `author`      |  `string`  | 作者名                                                |
| `level`       |   `int`    | 涩气级别，[详见level说明](#level)                     |
| `title`       |  `string`  | 作品标题                                              |
| `description` |  `string`  | 作品描述                                              |
| `r18`         | `boolean`  | 是否 包含R-18标签                                     |
| `gif`         | `boolean`  | 是否 动图，即包含动图标签                            |
| `original`    | `boolean`  | 是否 原图，pixiv作品中返回的一个标识                 |
| `width`       |   `int`    | 原图宽度 px                                           |
| `height`      |   `int`    | 原图高度 px                                           |
| `ext`         |  `string`  | 图片扩展名                                            |
| `uploadDate`  |   `int`    | 作品上传日期；时间戳，单位为毫秒                      |
| `urls`        |  `object`  | 包含了4种尺寸的图片地址                               |
| `tags`        | `string[]` | 作品标签，包含标签的中文翻译（有的话）                |
| `extags`      | `string[]` | 扩展标签，指本人额外添加的标签（如果有空添加的话）    |






