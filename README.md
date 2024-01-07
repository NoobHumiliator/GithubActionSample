# Github Action功能样例

原理：使用Github Action功能，运行python程序，实现无服务器的免费任务，比如天气推送，薅羊毛，签到

### 视频教程

作者：**技术爬爬虾**

> [!CAUTION]
>
> 本名称全网同名，转载时请注明原作者！

## Part1 构建画爱心为可执行程序

1. Fork 本项目。
2. 导航到 *Actions* 页面，启用 Actions 功能。
3. 选择左侧「画爱心」，选择右侧 "Run workflow" 启动流水线。
4. 等待流水线执行完毕，页面下方 *Artifacts* 将会得到4个可执行文件压缩包。

## Part2 天气推送

### 申请公众号测试账户

1. 访问 [此页面](https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login) ，使用微信扫码即可。
2. 在 *测试号信息* 部分，获取 `appID` 与 `appsecret` 值。
   ![image](https://github.com/tech-shrimp/FreeWechatPush/assets/154193368/bdb27abd-39cb-4e77-9b89-299afabc7330)
3. 想让谁收消息，谁就用微信扫二维码，此账号会自动添加到用户列表，获取微信号 `openId` 。
   ![image](https://github.com/tech-shrimp/FreeWechatPush/assets/154193368/1327c6f5-5c92-4310-a10b-6f2956c1dd75)
4. 新增测试模板,获得模板 ID `template_id` 。
   ![image](https://github.com/tech-shrimp/FreeWechatPush/assets/154193368/ec689f4d-6c0b-44c4-915a-6fd7ada17028)

   模板标题随便填，模板内容如下，可以根据需求自己定制：

   ```text
   今天：{{date.DATA}}
   地区：{{region.DATA}}
   天气：{{weather.DATA}}
   气温：{{temp.DATA}}
   风向：{{wind_dir.DATA}}
   对你说的话：{{today_note.DATA}}
   ```

### 项目配置

1. Fork 本项目。
2. 进入项目 *Settings* > *Secrets and variables* > *Actions* > *New repository secret* ，配置下图 4 项「秘密」环境变量。
   <img width="590" alt="image" src="https://github.com/tech-shrimp/GithubActionSample/assets/154193368/9e6b799d-9230-4d3e-8966-6c6f49e9b89f">
3. 进入自己项目的 *Action* > *天气预报推送* > `weather_report.yml` ，修改 `on.schedule.[*].cron` 表达式值。
   > [!CAUTION]
   > 
   > 此处 Cron 表达式使用 UTC 世界协调时，较北京时间慢8小时。
   <img width="503" alt="image" src="https://github.com/tech-shrimp/GithubActionSample/assets/154193368/badcc0fa-def5-428f-9238-fa6b549baefc">

## Part3 签到薅羊毛

1. Fork本项目
2. 浏览器访问 [京东官网](https://jd.com/) ，使用 <kbd>F12</kbd> 打开控制台，点击 **切换模式** 并切换到手机模式，刷新页面。
   ![image](https://github.com/tech-shrimp/GithubActionSample/assets/154193368/44d01795-8c1e-4a56-bb0e-a36f74062dcb)
3. 在 *网络* > `m.jd.com` 找到 Cookie
   <img width="935" alt="image" src="https://github.com/tech-shrimp/GithubActionSample/assets/154193368/97139add-a410-4e73-82d3-055c8136ed57">
4. 将其填入 *Settings*  > *Secrets and variables* > *Actions* > *New repository secret*
   <img width="685" alt="image" src="https://github.com/tech-shrimp/GithubActionSample/assets/154193368/e28ee156-642a-4c25-94ff-d42af072aa15">
5. 进入 *Action*  > *签到薅羊毛*  > `daily_sign.yml` ，修改 Cron 表达式的执行时间。
