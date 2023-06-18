# sd-webui-prompt-base
### 提升画面质量的提示词
HDR, HD，UHD, 64K (HDR、UHD、4K、8K和64K)  
表示图片效果，带来的改变可以试试，不过也会影响渲染出图的时间，会根据你要求的画面质量延长时间。  
Highly detailed 增加很多的细节，有时候描述没有那么多，随手丢进去，它会补细节。  
Studio lighting 添加和谐的靠谱一些的灯光效果，小概率加一些纹理  
Professional 会帮助自动调节对比度，色彩的和谐程度  
Vivid Colors 会帮忙增加一些鲜艳的颜色，比如用画中国画高级的配色，希望用到景泰蓝，经常会出现有点雾蒙蒙的，加入后会增强颜色的纯度和饱和度。  
Bokeh 画人像可以多尝试用这个词语，会比较突出人像  
high quality 高品质  
masterpiece 杰出  
best quality 最好品质  
photography 摄影作品  
ultra highres 超高分辨率  
RAW photo 原始照片  
ultra-detailed  
finely detail  
highres  
8k wallpaper

### 常用的反向提示词
worst quality  
bad quality  
low quality  
normal quality  
lowres  
normal quality

### 小括号用法
小括号代表的是1.1倍，比如Exquisite Crown（精美的皇冠），加上（Exquisite Crown）就代表皇冠这个词语的权重变成1.1倍，(((Exquisite Crown)))，代表1.1x1.1x1.1，1.331倍。  
中括号用法：  
中括号代表的是降权，因为初始化的权重是1，用\[Exquisite Crown\]代表的是0.952倍。  
大括号用法：  
大括号代表的是1.05倍，展示方式{Exquisite Crown}。  
注意：一般小括号用的比较多，可以用数字表示权重，这样就不需要中括号和大括号，比如Exquisite Crown：1.331）=(((Exquisite Crown)))

### 元素的融合  
方法一：中括号表示法  
\[pink|blond\]long hair，beautiful girl, gothic dress, clear details, Gothic architecture interior  
在这个里面的\[pink|blond\]long hair，用中括号将颜色隔开，渲染的时候，是一步粉红一步金色，最后出来的是调节过后的粉金色。中括号起到了混合的作用，同理，我们还可以用在服装材质、款式、背景玄幻...除了用中括号，另外还可以用and来连接，这是更细致的写法，可以用来规定某一个你想要混合的色彩的权重。  
方法二：AND  
pink long hair AND blond long hair，beautiful girl, gothic dress, clear details, Gothic architecture interior  
方法三：  
此方法被称作为元素渐变。可以通过混合两个关键词来实现更有趣效果，使用语法为“\[keyword1 : keyword2: factor\]”，其中factor值控制了把keyword1切换到keyword2的步骤值，是一个介于0到1之间的数字。  
举个例子，输入提示词“Oil painting portrait of \[Joe Biden: Donald Trump: 0.5\]”，采样步数设置为30。这里指的是，第1~15步，提示词为“Oil painting portrait of Joe Biden”；第16~30步，提示词为“Oil painting portrait of Donald Trump”。解释一下，factor值决定了关键词的切换节点，设置为0.5时指的是在30\*0.5 = 15步时切换。

### 元素的精细控制
使用\[keyword:number\]方式表示  
\[flower:5\],long blond hair, beautiful girl, gothic dress, clear details, Gothic architecture interior  
\[flower:5\]的意思是从第5步开始画花花，直到结束，以降低画的步数来达到弱化的效果。  
但是这也有个局限，在我们画画步数本来就不高的情况下，很容易画不出来，它没办法只用10步或15步给画出来的时候，往往不理你。  
此外，还有一些采样会不太搭理这种写法，可以探索看看。  
小黑板：  
\[flower:5\] 代表从第5步开始直到结束  
\[flower::10\] 代表从开始就一起画，但是画到第10步就不画了  
\[\[flower::30\]:5\] 代表从第5步开始画，到30步结束  
长呼一口浊气，试想一下，如果我们在画画的时候，写tag能够这样精细控制，熟练掌握各个元素出现的轻重，出来的画面能多细致。

### 画面的比重控制
上面是控制某一个东西的比重，下面来扒画面的比重。  
但是这是需要很长的步数来表现的，我今天用的不画那么多步，就写一下怎么表示。  
比如说我们将步数设定在100，前面50步用来画人，后面50步用来画花花。  
\[girl：flower：0.5\]，这样就表示前面的50%步数是画人的，后面的用来画花，人就会画到50步就结束了；  
另外一种就是直接写步数，据说可以这样用，但是我觉得并不好用，写法：\[girl:flower:50\]，在总步数100的时候，前面50用来画人，后面的画花。  
只是两种写法不一样，亲测下面的不如上面的写法好用。

### 元素随机选择
这个在批量生成的时候会好用一些，一张两张的体现不出。  
这里用到的是大括号。  
之前的tag：  
Long blond hair, beautiful girl, gothic dress, clear details, Gothic architecture interior  
之后的tag：  
{Crown|Corolla|Hairpin|Bowknot}，long blond hair, beautiful girl, gothic dress, clear details, Gothic architecture interior

  
### 词汇顺序/数量/位置影响
早期的标记具有更一致的位置，因此神经网络更容易预测它们的相关性。而且由于attention机制的特殊性，每次训练时，开始的标记和结束的标记总会被注意到（attention）。而且由于标记越多，单个标记被被注意到的概率越低。  
基于以上特性，有以下几点需要注意：

开头与结尾的词往往作用性更强。  
提示词数量越多，单个提示词的作用性越低。  
开头的数个提示词的作用较强，有更强的相关。  
关于数量，你可能已经注意到了，当你写prompt时会有数量限制。  
但是在 webui中，你是可以写 75 个词汇以上的提示的。webui会自动通过对提示词进行分组。当提示超过 75 个 token（可以理解token代表你的提示词），提交多组 75 个 token。单个token只具有同一组中其他内容的上下文。  
每一组都会被补充至(1,77,768)的张量，然后进行合并，比如俩组就会合并为(1,154,768)的张量，然后被送入U-Net。  
值得注意的是  
为了避免将你的短语分成俩组，webui在分组时会查看附近是否有,来尽量还原你想要的输入。  
然后你还能通过输入BREAK来快速分组，BREAK必须为大写。

### 参考文献：  
> https://zhuanlan.zhihu.com/p/626136427  
> https://openai.wiki/stable-diffusion-prompt.html
