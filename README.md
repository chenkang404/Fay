<div align="center">
    <br>
    <img src="images/icon.png" alt="Fay">
    <h1>FAY</h1>
	<h3>Fay数字人助理</h3>
</div>


Fay数字人助理版是fay开源项目的重要分支，专注于构建智能数字助理的开源解决方案。它提供了灵活的模块化设计，使开发人员能够定制和组合各种功能模块，包括情绪分析、NLP处理、语音合成和语音输出等。Fay数字人助理版为开发人员提供了强大的工具和资源，用于构建智能、个性化和多功能的数字助理应用。通过该版本，开发人员可以轻松创建适用于各种场景和领域的数字人助理，为用户提供智能化的语音交互和个性化服务。

## **推荐集成**

消费级pc大模型（ChatGLM-6B的基础上前置Rasa会话管理）：https://m.bilibili.com/video/BV1D14y1f7pr 

UE5工程：https://github.com/xszyou/fay-ue5

视频三维重建（真人2D驱动）：https://github.com/waityousea/xuniren



## **Fay数字人助理版**

注：带货版移到分支[`fay-sales-edition`](https://github.com/TheRamU/Fay/tree/fay-sales-edition)

![](images/controller.png)



### **PC远程助理**   [`PC demo`](https://github.com/TheRamU/Fay/tree/main/python_connector_demo)

### **手机远程助理**  [`android demo`](https://github.com/TheRamU/Fay/tree/main/android_connector_demo)




### **与数字形象通讯**（非必须,控制器需要关闭“面板播放”）

控制器与采用 WebSocket 方式与 UE 通讯

![](images/cs.png)

下载工程: [https://pan.baidu.com/s/1RBo2Pie6A5yTrCf1cn_Tuw?pwd=ck99](https://pan.baidu.com/s/1RBo2Pie6A5yTrCf1cn_Tuw?pwd=ck99)


下载windows运行包: [https://pan.baidu.com/s/1CsJ647uV5rS2NjQH3QT0Iw?pwd=s9s8](https://pan.baidu.com/s/1CsJ647uV5rS2NjQH3QT0Iw?pwd=s9s8)

![](images/UElucky.png)

工程及运行包：https://github.com/xszyou/fay-ue5

通讯地址: [`ws://127.0.0.1:10002`](ws://127.0.0.1:10002)（已接通）

消息格式: 查看 [WebSocket.md](https://github.com/TheRamU/Fay/blob/main/WebSocket.md)



### **与远程音频输入输出设备连接**（非必须,外网需要配置http://ngrok.cc tcp通道的clientid）

控制器与采用 socket(非websocket) 方式与 音频输出设备通讯

内网通讯地址: [`ws://127.0.0.1:10001`](ws://127.0.0.1:10001)

外网通讯地址: 通过http://ngrok.cc获取（有伙伴愿意赞助服务器给社区免费使用吗？）

![](images/Dingtalk_20230131122109.jpg)
消息格式: 参考 [remote_audio.py](https://github.com/TheRamU/Fay/blob/main/python_connector_demo/remote_audio.py)




## **二、Fay控制器核心逻辑**

![](images/luoji.png)

 **注：**

以上每个模块可轻易替换成自家核心产品。


### **目录结构**

```
.
├── main.py					# 程序主入口
├── fay_booter.py			# 核心启动模块
├── config.json				# 控制器配置文件
├── system.conf				# 系统配置文件
├── ai_module
│   ├── ali_nls.py			# 阿里云 实时语音
│   ├── ms_tts_sdk.py       # 微软 文本转语音
│   ├── xf_aiui.py          # 讯飞 人机交互-自然语言处理
│   ├── chatgpt.py          # gpt3.5对接
│   ├── yuan_1_0.py          # 浪潮.源大模型对接
│   ├── nlp_rasa.py          # ChatGLM-6B的基础上前置Rasa会话管理(强烈推荐)
│   └── xf_ltp.py           # 讯飞 情感分析
├── bin                     # 可执行文件目录
├── core                    # 数字人核心
│   ├── fay_core.py         # 数字人核心模块
│   ├── recorder.py         # 录音器
│   ├── tts_voice.py        # 语音生源枚举
│   ├── viewer.py           # 抖音直播间接入模块
│   └── wsa_server.py       # WebSocket 服务端
├── gui                     # 图形界面
│   ├── flask_server.py     # Flask 服务端
│   ├── static
│   ├── templates
│   └── window.py           # 窗口模块
├── scheduler
│   └── thread_manager.py   # 调度管理器
└── utils                   # 工具模块
    ├── config_util.py      
    ├── storer.py
    └── util.py
```


## **三、升级日志**

**2023.05.12：**

+ 打出Fay数字人助理版作为主分支（带货版移到分支[`fay-sales-edition`](https://github.com/TheRamU/Fay/tree/fay-sales-edition)）；
+ 添加Fay助理的文字沟通窗口（文字与语音同步）；
+ 添加沟通记录本地保存功能；
+ 升级ChatGLM-6B的应用逻辑，长文本与语音回复分享；


## **四、安装说明**


### **环境** 
- Python 3.8、3.9、3.10
- Windows、macos、linux

### **安装依赖**

```shell
pip install -r requirements.txt
```

### **配置应用密钥**
+ 查看 [AI 模块](#ai-模块)
+ 浏览链接，注册并创建应用，将应用密钥填入 `./system.conf` 中

### **启动**
启动Fay控制器
```shell
python main.py
```


### **AI 模块**
启动前需填入应用密钥

| 代码模块                  | 描述                       | 链接                                                         |
| ------------------------- | -------------------------- | ------------------------------------------------------------ |
| ./ai_module/ali_nls.py    | 阿里云 实时语音识别        | https://ai.aliyun.com/nls/trans                              |
| ./ai_module/ms_tts_sdk.py | 微软 文本转情绪语音（可选）   | https://azure.microsoft.com/zh-cn/services/cognitive-services/text-to-speech/ |
| ./ai_module/xf_ltp.py     | 讯飞 情感分析              | https://www.xfyun.cn/service/emotion-analysis                |
| ./utils/ngrok_util.py     | ngrok.cc 外网穿透（可选）  | http://ngrok.cc                                              |
| ./ai_module/yuan_1_0.py    | 浪潮源大模型（NLP 4选1）  | https://air.inspur.com/                                              |
| ./ai_module/chatgpt.py     | ChatGPT（NLP 4选1）  | *******                                              |
| ./ai_module/xf_aiui.py    | 讯飞自然语言处理（NLP 4选1）   | https://aiui.xfyun.cn/solution/webapi                        |
| ./ai_module/nlp_rasa.py    | ChatGLM-6B的基础上前置Rasa会话管理（NLP 4选1）   | https://m.bilibili.com/video/BV1D14y1f7pr |



## **五、使用说明**


### **使用说明**

+ 语音助理：fay控制器（麦克风输入源开启、面板播放开启）；
+ 远程语音助理：fay控制器（面板播放关闭）+ 远程设备接入；
+ 数字人互动：fay控制器（麦克风输入源开启、面板播放关闭、填写性格Q&A）+ 数字人；
+ 贾维斯、Her：加入我们一起完成。


### **语音指令**

| 关闭核心                  | 静音                       | 取消静音                                                         |
| ------------------------- | -------------------------- | ------------------------------------------------------------ |
| 关闭、再见、你走吧   | 静音、闭嘴、我想静静        |   取消静音、你在哪呢、你可以说话了                            |

| 播放歌曲(音乐库暂不可用)                  | 暂停播放                       | 更多                                                         |
| ------------------------- | -------------------------- | ------------------------------------------------------------ |
| 播放歌曲、播放音乐、唱首歌、放首歌、听音乐、你会唱歌吗   | 暂停播放、别唱了、我不想听了        |     没有了...                          |

### **人设**
数字人属性，与用户交互中能做出相应的响应。
#### 交互灵敏度
在交互中，数字人能感受用户的情感，并作出反应。最直的体现，就是语气的变化，如 开心/伤心/生气 等。
设置灵敏度，可改变用户情感对于数字人的影响程度。

### **接收来源**

#### 文本输入

通过沟通窗口与助理文本沟通

#### 麦克风

选择麦克风设备，实现面对面交互，成为你的伙伴

#### socket远程音频输入

可以接入远程音频输入，远程音频输出



### 相关文章：
1、集成消费级pc大模型（ChatGLM-6B的基础上前置Rasa会话管理）：https://m.bilibili.com/video/BV1D14y1f7pr 

2、[(34条消息) 非常全面的数字人解决方案_郭泽斌之心的博客-CSDN博客_数字人算法](https://blog.csdn.net/aa84758481/article/details/124758727)

3、【开源项目：数字人FAY——Fay新架构使用讲解】 https://www.bilibili.com/video/BV1NM411B7Ab/?share_source=copy_web&vd_source=64cd9062f5046acba398177b62bea9ad

4、【开源项目FAY——UE工程讲解】https://www.bilibili.com/video/BV1C8411P7Ac?vd_source=64cd9062f5046acba398177b62bea9ad

5、m1机器安装办法（Gason提供）：https://www.zhihu.com/question/437075754

6、bilbil主页：[xszyou的个人空间_哔哩哔哩_bilibili](https://space.bilibili.com/2111554564)



商务联系QQ 467665317，我们提供：开发顾问、数字人模型定制及高校教学资源实施服务
http://yafrm.com/forum.php?mod=viewthread&tid=302

关注公众号获取最新微信技术交流群二维码（**请先star本仓库**）

![](images/gzh.jpg)





