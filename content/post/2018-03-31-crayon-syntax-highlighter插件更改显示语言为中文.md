---
title: Crayon Syntax Highlighter插件更改显示语言为中文
author: 3mile
type: post
date: 2018-03-31T06:48:38+00:00
url: /archives/986
newslite-default-layout:
  - right-sidebar
newslite-single-post-image-align:
  - full
categories:
  - 博客系统
thumbnailImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/4.jpg
# 封面图像相对路径
coverImage: https://mile3-1253674458.cos.ap-chengdu.myqcloud.com/assets/cover/4.jpg
#封面说明内容
coverCaption: "A beautiful cover"
#标题在封面内(in),还是封面外(out)
coverMeta: in
# partial（60％）		full，：封面图片占整个屏幕的高度。
coverSize: partial

comment: true
---
<fieldset>
  <legend>Crayon Syntax Highlighter</legend> 
  
  <p>
    Crayon Syntax Highlighter是一个强大的代码高亮插件，强大的地方主要是它拥有多种高亮主题和多种显示字体来展示代码让使用者有足够多的搭配选择，另一方面就是其加载速度快，可以解析代码中的html，并且着色效果更好。安装的方法很简单只要在wordpress后台搜索名称安装设置即可。</fieldset> 
    
    <h2>
    </h2>
    
    <h2>
      实例效果：
    </h2>
    
    <div id="crayon-5abf2cf9c084f024894327" class="crayon-syntax crayon-theme-ado crayon-font-monaco crayon-os-pc print-yes notranslate crayon-wrapped" data-settings=" minimize scroll-mouseover wrap">
      <div class="crayon-plain-wrap">
      </div>
      
      <div class="crayon-main">
        <pre class="lang:default decode:true ">CMemPoolMgr::CMemPoolMgr(unsigned int poolsize         /* = DEFAULT_POOLSIZE */,   
        unsigned int poolunitsize     /* = DEFAULT_POOLUNITSIZE */,  
        unsigned int blockunitsize    /* = DEFAULT_BLOCKUNITSIZE */)  
    {  
        m_nPoolSize         = poolsize;  
        m_nPoolUnitSize     = poolunitsize;  
        m_nBlockUnitSize    = blockunitsize;  
 
        m_nTotalMemPool     = 0;  
        m_nUsingMemPool     = 0;  
 
        m_TimeTick          = GetTickCount();  
 
#ifdef _DEBUG  
        m_nCode             = 0;  
#endif  
    }</pre>
        
        <p>
          &nbsp;
        </p>
      </div>
    </div>
    
    <h2>
    </h2>
    
    <h2>
      安装后显示语言为英文的问题
    </h2>
    
    <p>
      明明插件有中文翻译文件但是自己的博客中却显示是英文，找了好多种解决方法终于被我发现了Crayon翻译成中文的方法，亲测有效，下面是转载内容：
    </p>
    
    <p>
      安装了Crayon Syntax Highlighter之后发现无论是设置页面还是可视化编辑页面都是英文的，然后Crayon Syntax Highlighter的语言文件发现汉化文件存在，但是
    </p>
    
    <p>
      <span style="color: #ff0000;"><code>wp-content/languages/plugins/</code></span>
    </p>
    
    <p>
      <span style="color: #ff0000;"><code></code></span>中的汉化文件却是不完整的。
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      解决方法
    </h2>
    
    <p>
      1、找到Crayon Syntax Highlighter插件位置
    </p>
    
    <div id="sc_warn">
      <code>&lt;span style="color: #ff0000;">wp–content/plugins/crayon–syntax–highlighter/&lt;/span></code>
    </div>
    
    <div>
      找到语言文件目录：trans<br /> 找到中文文件：</p> 
      
      <div id="sc_xuk">
        <span style="color: #ff0000;"><code>crayon-syntax-highlighter-zh_CN.mo</code></span><br /> <span style="color: #ff0000;"> <code>crayon-syntax-highlighter-zh_CN.po</code></span>
      </div>
      
      <div>
      </div>
    </div>
    
    <p>
      2、将上面的中文文件从服务器上下载下来，然后上传到
    </p>
    
    <p>
      <code>&lt;span style="color: #ff0000;">/wp–content/languages/plugins/&lt;/span></code>
    </p>
    
    <p>
      进行文件的覆盖，完成后刷新页面就会发现插件的页面语言已经修改为中文了。
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      问题成功解决。
    </p>