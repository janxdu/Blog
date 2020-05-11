---
title: 博客双部署及引入评论功能
date: 2018-05-28 00:00:00
---
<body itemscope itemtype="http://schema.org/WebPage" lang="en">

  
  
    
  

  <div class="container sidebar-position-right page-post-detail">
    <div class="headband"></div>

    <header id="header" class="header" itemscope itemtype="http://schema.org/WPHeader">
      <div class="header-inner"><div class="site-brand-wrapper">
  <div class="site-meta ">
    

    <div class="custom-logo-site-title">
      <a href="/"  class="brand" rel="start">
        <span class="logo-line-before"><i></i></span>
        <span class="site-title">Jan Du</span>
        <span class="logo-line-after"><i></i></span>
      </a>
    </div>
      
        <h1 class="site-subtitle" itemprop="description">Pain+Reflection=Progress</h1>
      
  </div>

  <div class="site-nav-toggle">
    <button>
      <span class="btn-bar"></span>
      <span class="btn-bar"></span>
      <span class="btn-bar"></span>
    </button>
  </div>
</div>

<nav class="site-nav">
  

  
    <ul id="menu" class="menu">
      
        
        <li class="menu-item menu-item-home">
          <a href="/" rel="section">
            
              <i class="menu-item-icon fa fa-fw fa-question-circle"></i> <br />
            
            Home
          </a>
        </li>
      
        
        <li class="menu-item menu-item-categories">
          <a href="/categories" rel="section">
            
              <i class="menu-item-icon fa fa-fw fa-question-circle"></i> <br />
            
            Categories
          </a>
        </li>
      
        
        <li class="menu-item menu-item-archives">
          <a href="/archives" rel="section">
            
              <i class="menu-item-icon fa fa-fw fa-question-circle"></i> <br />
            
            Archives
          </a>
        </li>
      
        
        <li class="menu-item menu-item-tags">
          <a href="/tags" rel="section">
            
              <i class="menu-item-icon fa fa-fw fa-question-circle"></i> <br />
            
            Tags
          </a>
        </li>
      

      
    </ul>
  

  
</nav>



 </div>
    </header>

    <main id="main" class="main">
      <div class="main-inner">
        <div class="content-wrap">
          <div id="content" class="content">
            

  <div id="posts" class="posts-expand">
    

  

  
  
  

  <article class="post post-type-normal" itemscope itemtype="http://schema.org/Article">
  
  
  
  <div class="post-block">
    <link itemprop="mainEntityOfPage" href="https://jandu.me/2018/05/28/BlogAddDualDeploymentAndCommentFunction/">

    <span hidden itemprop="author" itemscope itemtype="http://schema.org/Person">
      <meta itemprop="name" content="Jan Du">
      <meta itemprop="description" content="">
      <meta itemprop="image" content="/images/avatar.gif">
    </span>

    <span hidden itemprop="publisher" itemscope itemtype="http://schema.org/Organization">
      <meta itemprop="name" content="Jan Du">
    </span>

    
      <header class="post-header">

        
        
          <h2 class="post-title" itemprop="name headline">博客双部署及引入评论功能</h2>
        

        <div class="post-meta">
          <span class="post-time">
            
              <span class="post-meta-item-icon">
                <i class="fa fa-calendar-o"></i>
              </span>
              
                <span class="post-meta-item-text">Posted on</span>
              
              <time title="Post created" itemprop="dateCreated datePublished" datetime="2018-05-28T23:42:51+08:00">
                2018-05-28
              </time>
            

            
              <span class="post-meta-divider">|</span>
            

            
              <span class="post-meta-item-icon">
                <i class="fa fa-calendar-check-o"></i>
              </span>
              
                <span class="post-meta-item-text">Post modified&#58;</span>
              
              <time title="Post modified" itemprop="dateModified" datetime="2018-06-07T19:47:54+08:00">
                2018-06-07
              </time>
            
          </span>

          
            <span class="post-category" >
            
              <span class="post-meta-divider">|</span>
            
              <span class="post-meta-item-icon">
                <i class="fa fa-folder-o"></i>
              </span>
              
                <span class="post-meta-item-text">In</span>
              
              
                <span itemprop="about" itemscope itemtype="http://schema.org/Thing">
                  <a href="/categories/Journal/" itemprop="url" rel="index">
                    <span itemprop="name">Journal</span>
                  </a>
                </span>

                
                
              
            </span>
          

          
            
              <span class="post-comments-count">
                <span class="post-meta-divider">|</span>
                <span class="post-meta-item-icon">
                  <i class="fa fa-comment-o"></i>
                </span>
                <a href="/2018/05/28/BlogAddDualDeploymentAndCommentFunction/#comments" itemprop="discussionUrl">
                  <span class="post-comments-count disqus-comment-count"
                        data-disqus-identifier="2018/05/28/BlogAddDualDeploymentAndCommentFunction/" itemprop="commentCount"></span>
                </a>
              </span>
            
          

          
          
             <span id="/2018/05/28/BlogAddDualDeploymentAndCommentFunction/" class="leancloud_visitors" data-flag-title="博客双部署及引入评论功能">
               <span class="post-meta-divider">|</span>
               <span class="post-meta-item-icon">
                 <i class="fa fa-eye"></i>
               </span>
               
                 <span class="post-meta-item-text">Visitors&#58;</span>
               
                 <span class="leancloud-visitors-count"></span>
             </span>
          

          

          

          

        </div>
      </header>
    

    
    
    
    <div class="post-body" itemprop="articleBody">

      
      

      
        <p>博客原来部署在Github Pages上，由于众所周知的原因，访问速度十分不稳定，严重影响阅读体验。而且由于第三方的评论平台一直在不断关闭，所以一直没有引入评论功能。这次把它们一起解决。</p>
<h3 id="部署到Coding-net"><a href="#部署到Coding-net" class="headerlink" title="部署到Coding.net"></a>部署到Coding.net</h3><ol>
<li>创建项目。在Coding.net创建一个项目名为 yourname.coding.me 的项目（yourname为实际用户名）。在该项目的代码tab页，勾选快速初始化（生成README.md），选择默认分支master。</li>
<li>SSH Key生成及部署。<br>由于我的Coding.net账户和Github账户绑定同一邮箱，想复用原来的Key，但是passphrase已经忘记了，无奈需要创建一个新Key，passphrase设置为空。本地命令行执行以下命令<figure class="highlight plain"><table><tr><td class="gutter"><pre><div class="line">1</div><div class="line">2</div><div class="line">3</div><div class="line">4</div><div class="line">5</div><div class="line">6</div><div class="line">7</div><div class="line">8</div><div class="line">9</div></pre></td><td class="code"><pre><div class="line">// 生成SSH Key</div><div class="line">$ ssh-keygen -t rsa -b 4096 -C &quot;your_email@example.com&quot;</div><div class="line">// 可自定义Key文件名</div><div class="line">$ Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]</div><div class="line">// 可输入passphrase</div><div class="line">$ Enter passphrase (empty for no passphrase): [Type a passphrase]</div><div class="line">$ Enter same passphrase again: [Type passphrase again]</div><div class="line">// 将公钥复制到剪贴板</div><div class="line">$ pbcopy &lt; ~/.ssh/id_rsa.pub</div></pre></td></tr></table></figure>
</li>
</ol>
<p>拿到公钥之后就可以到Coding.net的账户-SSH公钥tab页新增公钥配置了。配置完成后本地验证连通性，如果结果为success即部署成功。<br><figure class="highlight plain"><table><tr><td class="gutter"><pre><div class="line">1</div></pre></td><td class="code"><pre><div class="line">$ ssh -T git@git.coding.net</div></pre></td></tr></table></figure></p>
<ol>
<li><p>Hexo配置更新<br>我使用Hexo模版引擎生成静态博客，本身支持多部署。修改本地项目仓库的<code>_config.yml</code>的<code>deploy</code>参数</p>
<figure class="highlight plain"><table><tr><td class="gutter"><pre><div class="line">1</div><div class="line">2</div><div class="line">3</div><div class="line">4</div><div class="line">5</div></pre></td><td class="code"><pre><div class="line">deploy:</div><div class="line">  type: git</div><div class="line">  repo: </div><div class="line">    github: git@github.com:your_name/your_name.github.io.git,master</div><div class="line">    coding: git@git.coding.net:your_name/your_name.coding.me,master</div></pre></td></tr></table></figure>
</li>
<li><p>正常部署Hexo验证结果</p>
<figure class="highlight plain"><table><tr><td class="gutter"><pre><div class="line">1</div></pre></td><td class="code"><pre><div class="line">$ hexo d</div></pre></td></tr></table></figure>
</li>
</ol>
<h3 id="引入Disqus评论"><a href="#引入Disqus评论" class="headerlink" title="引入Disqus评论"></a>引入Disqus评论</h3><p>由于博客没有备案，无法使用搜狐畅言的评论系统。故选择国外的Disqus，比较稳定。其官网需要科学上网才能访问，使用很方便，新建一个Disqus并设置Website Name即可。<br>本地项目使用了Next主题，本身支持Disqus评论，只需配置主题下<code>_config.yml</code>的<code>disqus</code>参数即可。</p>
<figure class="highlight plain"><table><tr><td class="gutter"><pre><div class="line">1</div><div class="line">2</div><div class="line">3</div><div class="line">4</div></pre></td><td class="code"><pre><div class="line">disqus:</div><div class="line">  enable: true</div><div class="line">  shortname: your_shortname</div><div class="line">  count: true</div></pre></td></tr></table></figure>
<p>此次双部署及评论引入中间还遇到Https失效，主题升级后样式错误等问题。最终都得以解决，还是一个很有意义的过程。</p>

      
    </div>
    
    
    

    

    

    

    <footer class="post-footer">
      

      
      
      

      
        <div class="post-nav">
          <div class="post-nav-next post-nav-item">
            
              <a href="/2018/05/21/FeelingOfTheSpecialPeople/" rel="next" title="特别人类给我的特别感受">
                <i class="fa fa-chevron-left"></i> 特别人类给我的特别感受
              </a>
            
          </div>

          <span class="post-nav-divider"></span>

          <div class="post-nav-prev post-nav-item">
            
              <a href="/2018/06/07/MorningRunning/" rel="prev" title="晨跑伊始">
                晨跑伊始 <i class="fa fa-chevron-right"></i>
              </a>
            
          </div>
        </div>
      

      
      
    </footer>
  </div>
  
  
  
  </article>



    <div class="post-spread">
      
    </div>
  </div>


          </div>
          


          

  
    <div class="comments" id="comments">
      <div id="disqus_thread">
        <noscript>
          Please enable JavaScript to view the
          <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a>
        </noscript>
      </div>
    </div>

  



        </div>
        
          
  
  <div class="sidebar-toggle">
    <div class="sidebar-toggle-line-wrap">
      <span class="sidebar-toggle-line sidebar-toggle-line-first"></span>
      <span class="sidebar-toggle-line sidebar-toggle-line-middle"></span>
      <span class="sidebar-toggle-line sidebar-toggle-line-last"></span>
    </div>
  </div>

  <aside id="sidebar" class="sidebar">
    
    <div class="sidebar-inner">

      

      
        <ul class="sidebar-nav motion-element">
          <li class="sidebar-nav-toc sidebar-nav-active" data-target="post-toc-wrap">
            Table of Contents
          </li>
          <li class="sidebar-nav-overview" data-target="site-overview-wrap">
            Overview
          </li>
        </ul>
      

      <section class="site-overview-wrap sidebar-panel">
        <div class="site-overview">
          <div class="site-author motion-element" itemprop="author" itemscope itemtype="http://schema.org/Person">
            
              <p class="site-author-name" itemprop="name">Jan Du</p>
              <p class="site-description motion-element" itemprop="description"></p>
          </div>

          <nav class="site-state motion-element">

            
              <div class="site-state-item site-state-posts">
              
                <a href="/archives">
              
                  <span class="site-state-item-count">69</span>
                  <span class="site-state-item-name">posts</span>
                </a>
              </div>
            

            
              
              
              <div class="site-state-item site-state-categories">
                <a href="/categories/index.html">
                  <span class="site-state-item-count">6</span>
                  <span class="site-state-item-name">categories</span>
                </a>
              </div>
            

            
              
              
              <div class="site-state-item site-state-tags">
                <a href="/tags/index.html">
                  <span class="site-state-item-count">4</span>
                  <span class="site-state-item-name">tags</span>
                </a>
              </div>
            

          </nav>

          

          

          
          

          
          

          

        </div>
      </section>

      
      <!--noindex-->
        <section class="post-toc-wrap motion-element sidebar-panel sidebar-panel-active">
          <div class="post-toc">

            
              
            

            
              <div class="post-toc-content"><ol class="nav"><li class="nav-item nav-level-3"><a class="nav-link" href="#部署到Coding-net"><span class="nav-text">部署到Coding.net</span></a></li><li class="nav-item nav-level-3"><a class="nav-link" href="#引入Disqus评论"><span class="nav-text">引入Disqus评论</span></a></li></ol></div>
            

          </div>
        </section>
      <!--/noindex-->
      

      

    </div>
  </aside>


        
      </div>
    </main>

    <footer id="footer" class="footer">
      <div class="footer-inner">
        <div class="copyright">&copy; <span itemprop="copyrightYear">2018</span>
  <span class="with-love">
    <i class="fa fa-user"></i>
  </span>
  <span class="author" itemprop="copyrightHolder">Jan Du</span>

  
</div>









        







        
      </div>
    </footer>

    
      <div class="back-to-top">
        <i class="fa fa-arrow-up"></i>
        
      </div>
    

    

  </div>

  

  




  




	





  














  





  




  

  

  
  

  

  

  

</body>
