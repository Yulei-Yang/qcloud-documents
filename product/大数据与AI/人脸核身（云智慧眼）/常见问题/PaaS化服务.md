### PaaS 化服务中，如何获取动作顺序与数字验证码？
您需要调用以下对应的接口，以获取动作顺序或数字验证码（**除地域信息外，无需传其他参数**）：
- [获取动作顺序](https://cloud.tencent.com/document/product/1007/31822)。
- [获取数字验证码](https://cloud.tencent.com/document/product/1007/31821)。

### PaaS 化服务中，传入视频大于5M，如何进行压缩？
视频格式：H264编码标准的视频格式（如mp4，mov，avi，webm），
分辨率支持270p ~ 1080p，(推荐 wxh=320x*)，视频大小不超过8M，
如果前端手机录制 H5 视频过大，推荐使用 ffmpeg 先进行压缩再传到核身服务中。

推荐压缩命令：`./ffmpeg -y -v error -i SRC_VIDEO_FILE_PATH -preset veryfast -b:v 1048576 -vf format=pix_fmts=yuv420p,fps=25,scale=320:-16  DEST_VIDEO_FILE_NAME（只需要调整SRC_VIDEO_FILE_PATH, DEST_VIDEO_FILE_NAME两个参数）`

### PaaS 化服务中，数字活体模式中的四位数字可否自定义？
不支持，四位数字需要调用 GetLiveCode 接口随机生成，调用接口可保证数字时实时生成而非事先规定，可以一定程度上防止攻击者提前录制相同数字的视频进行攻击。

### 接口并发是否有限制？
默认 QPS 限制100次/秒，如果客户评估不能满足需求，欢迎您 [点此链接](https://cloud.tencent.com/document/product/1007/56130) 扫描二维码添加腾讯云人脸核身小助手进行询问。

### 验证结果信息量太大时，如何拉取成功？

验证结果信息量太大时，会导致一次性拉取失败，您可以先单独拉取判断验证结果（InfoType 选1），如果需要视频或身份信息留底，再用234去拉取。
我们支持拉取验证过程中的所有数据，并支持异步拉取，token 有效期为生成后的3天，3天内可多次拉取，建议分次拉取信息。

### 图片或视频转 Base64 时出错如何处理?

图片或视频转 Base64 时，需要去掉相关前缀`data:image/jpg;base64,`和换行符`\n`。

### 银行卡二要素、三要素、四要素，运营商三要素类接口产品是否支持外籍人士核验功能？	

暂不支持。

### 调用参数里面有地域选择这个参数，选择哪个地方有没有实质的影响？

1. 域名中的地域信息决定访问的是哪个接入点：`faceid.ap-shanghai.tencentcloudapi.com`就是要访问上海这个接入点。
2. 公共参数 Region 决定的是要访问业务资源所在区，例如 Region=ap-beijing 就是要操作北京区的资源。
   如果域名中不指定地域信息则是就近接入 。就近接入可能会存在问题。如果解析不到 IP 会默认到广州地域里面。另外域名地域和公共参数 Region 可以不一致 但是可能会增加耗时。建议客户域名和公共参数 Region 选择相同的地域。
   (建议域名和公共参数 Region 统一使用 ap-guangzhou )
<br>
<br>
<p align="right"><strong>问题没有解决，到 <a href="https://aistudio.cloud.tencent.com/faq"> AI Studio 技术答疑专题</a> 看看？</strong></p>
