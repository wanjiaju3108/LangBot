# QChatGPT

通过调用OpenAI GPT-3模型提供的Completion API来实现一个更加智能的QQ机器人  
已部署的测试机器人QQ: 960164003  
交流群、答疑群: 204785790  
无需云服务器，在个人电脑上即可部署

## 技术栈

- [Mirai](https://github.com/mamoe/mirai) 高效率 QQ 机器人支持库
- [YiriMirai](https://github.com/YiriMiraiProject/YiriMirai) 一个轻量级、低耦合的基于 mirai-api-http 的 Python SDK。
- PyMySQL MySQL驱动
- [OpenAI API](https://openai.com/api/) OpenAI API

## 项目结构

- `pkg.database` 数据库操作相关
  - 数据库用于存放会话的历史记录，确保在程序重启后能记住刚刚进行的对话内容
- `pkg.openai` OpenAI API相关
  - 用于调用OpenAI的API生成回复内容
- `pkg.qqbot` QQ机器人相关
  - 处理QQ收到的消息，调用API并进行回复

## 部署

- 请使用Python 3.9.x以上版本
- 建议使用MySQL 8.0以上版本
- 请注意OpenAI账号额度消耗
  - 每个账户仅有18美元免费额度，如未绑定银行卡，则会在超出时报错
  - OpenAI收费标准：默认使用的`text-davinci-003`模型 0.02美元/千字

### 1. 注册OpenAI账号并取得api_key

参考以下文章

- [只需 1 元搞定 ChatGPT 注册](https://zhuanlan.zhihu.com/p/589470082)
- [手把手教你如何注册ChatGPT，超级详细](https://guxiaobei.com/51461)

注册成功后请前往[个人中心查看](https://beta.openai.com/account/api-keys)api_key

### 2. 配置Mirai

按照[此教程](https://yiri-mirai.wybxc.cc/tutorials/01/configuration)配置Mirai及YiriMirai

### 3. 配置MySQL数据库

安装MySQL数据库，创建数据库`qchatgpt`

### 4. 配置此程序

1. 克隆此项目

```bash
git clone https://github.com/RockChinQ/QChatGPT
```

2. 安装依赖

```bash
pip3 install pymysql yiri-mirai openai colorlog func_timeout
```

3. 运行一次主程序，生成配置文件

```bash
python3 main.py
```

4. 编辑配置文件`config.py`

按照文件内注释填写配置信息

5. 初始化数据库

```bash
python3 main.py init_db
```

6. 运行主程序

- 如提示安装`uvicorn`或`hypercorn`请*不要*安装，这两个不是必需的，目前存在未知原因bug

```bash
python3 main.py
```

- 如报错`TypeError: As of 3.10, the *loop* parameter was removed from Lock() since it is no longer necessary`, 请参考 [此处](https://github.com/RockChinQ/QChatGPT/issues/5)

无报错信息即为运行成功

## 使用

### 私聊使用

1. 添加机器人QQ为好友
2. 发送消息给机器人，机器人即会自动回复
3. 可以通过`!help`查看帮助信息

<img alt="私聊示例" src="res/屏幕截图%202022-12-08%20150949.png" width="550" height="279"/>

### 群聊使用

1. 将机器人拉进群
2. at机器人并发送消息，机器人即会自动回复
3. at机器人并发送`!help`查看帮助信息

<img alt="群聊示例" src="res/屏幕截图%202022-12-08%20150511.png" width="671" height="522"/>