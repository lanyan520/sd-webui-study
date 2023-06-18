# sd-webui-prompt-base

SD绘画的prompt基础知识学习
-----------------------------------------------------
### 提升画面质量的提示词

最基本的常用的的关键词

> masterpiece 杰出  
> best quality 最好品质  
> high quality 高品质  
> highres  高分辨率（可选项）
> ultra highres 超高分辨率 （可选项）
> RAW photo （相机拍摄的图一般都会设定raw格式，它能更好的记录细节方便后期还原，可选项）
> 8k wallpaper （8k壁纸，可选项）
> finely detail  精细的细节
> ultra-detailed  超细节
> photography 摄影作品  
> Highly detailed 增加很多的细节，有时候描述没有那么多，随手丢进去，它会补细节
> Studio lighting 添加和谐的靠谱一些的灯光效果，小概率加一些纹理  
> Professional 会帮助自动调节对比度，色彩的和谐程度
> Vivid Colors 会帮忙增加一些鲜艳的颜色，经常会出现有点雾蒙蒙的，加入后会增强颜色的纯度和饱和度。  
> Bokeh 画人像可以多尝试用这个词语，会比较突出人像  

如果对画质有特别的需求，可以考虑一下参数，不过也会影响渲染出图的时间

> HDR, HD，UHD, 64K (HDR、UHD、4K、8K和64K)  

### 常用的反向提示词

> worst quality 最差的质量
> bad quality  坏的质量
> low quality  低质量
> normal quality  正常的质量

反向提示词需要根据具体绘画需求写TAG，例如需要绘画一个人物，我们需要限制他的手、脸、腿，例如

> bad hand
> Twisted hand
> bad face 
> Twisted face
> bad leg
> Twisted leg
> 3 leg,4 leg,3 fingers,4 fingers,6fingers,7fingers,3 hand...

当然随着时间的沉淀，技术的累积，出现了embedding 更方便（需要自行去网站下载），例如 badhandv4、negative_hand等

### 小括号用法

> 小括号代表的是1.1倍，比如1 girl，加上（1 girl）就代表这个词语的权重变成1.1倍，(((1 girl)))，代表1.1x1.1x1.1，1.331倍
> 中括号代表的是降权，因为初始化的权重是1，用\[1 girl\]代表的是0.952倍
> 大括号代表的是1.05倍，展示方式{1 girl}

Tip:一般小括号用的比较多，可以用数字表示权重，这样就不需要中括号和大括号，比如1 girl：1.331）=(((1 girl)))

### 元素的融合  

1⃣️ 中括号表示法  

> \[pink|blond\]long hair

在这个里面的\[pink|blond\]long hair，用中括号将颜色隔开，渲染的时候，是一步粉红一步金色，最后出来的是调节过后的粉金色。中括号起到了混合的作用

2⃣️ and表示法

> pink long hair and blond long hair

3⃣️ 元素渐变
  
可以通过混合两个关键词来实现更有趣效果，使用语法

> “\[a : b: value\]”，其中factor值控制了把a切换到b的步骤值，是一个介于0到1之间的数字
>  假设采样步数 size=20
>  0-value*size步的提示词=a,value*size+1-size步的提示词=b
>  value决定的提示词切换时机

### 元素的精细控制

使用\[keyword:number\]方式表示  

> \[flower:5\] 的意思是从第5步开始画直到结束，以降低画的步数来达到弱化的效果
> \[flower::10\] 代表从开始就一起画，但是画到第10步就不画了  
> \[\[flower::30\]:5\] 代表从第5步开始画，到30步结束 
> 如果采样步数本就不高的情况下，可能他没法几步给画出来

### 画面的比重控制

画面的比重控制需要很长的采样步数，就简单介绍一下
> \[girl：flower：0.5\]，这样就表示前面的50%步数是画人的，后面的用来画花
> \[girl:flower:50\]，在总步数100的时候，前面50用来画人，后面的画花。  

### 元素随机选择

这个在批量生成的时候会好用一些，同一个种子不同的画风
> {long hair|short hair|black hair|pink hair}
  
### 词汇顺序/数量/位置影响

> 开头与结尾的词往往作用性更强
> 提示词数量越多，单个提示词的作用性越低
> 开头的数个提示词的作用较强，有更强的相关
> 关于数量，你可能已经注意到了，当你写prompt时会有数量限制
> 但是在 webui中，你是可以写 75 个词汇以上的提示的,webui会自动通过对提示词进行分组

### 参考文献：  
> https://zhuanlan.zhihu.com/p/626136427  
> https://openai.wiki/stable-diffusion-prompt.html
