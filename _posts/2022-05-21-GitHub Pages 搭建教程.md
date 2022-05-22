---
layout: post
title: "GitHub Pages博客搭建教程"
date: 2022-05-20
tags: [成长, 总结, 博客]
description: [github docs搭建博客入门，及遇到的问题]
---

## 为什么使用 GitHub Pages

如果你把他作为一个轻量级的个人博客服务，GitHub Pages 相较 WordPress 之类的建站服务有什么优势呢？

- 首先他是完全免费的，相较其他的同类产品，他能替你省下一笔服务费，节约下的钱可以让你买一些其他的会员服务；
- 无须自己购买云服务进行搭建，只需按步骤一步步操作即可，即使你不懂他的技术细节；
- 支持的功能多，玩法丰富，你可以绑定你的域名、使用免费的 HTTPS、自己 DIY 网站的主题、使用他人开发好的插件等等；
- 当完成搭建后，你只需要专注于文章创作就可以了，其他诸如环境搭建、系统维护、文件存储的事情一概不用操心，都由 GitHub 处理

当然了，作为一款免费的服务，我们也是要遵守 GitHub 官方使用建议和限制，在使用的时候项目和网站的大小不要超过 1GB，也不要过于频繁的更新网站的内容（每小时不超过 10 个版本），每个月的也要注意带宽使用上限为 100GB。

综合来看，GitHub Pages 依旧可以说是中小型博客或项目主页的最佳选项之一。

## 如何使用 GitHub pages

介绍了这么多，下面就具体来谈谈如何使用它。

### 基本页面的生成

首先你需要注册一个 GitHub 账号，并在个人主界面里选择创建一个新的 Repository 。

![img](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ds2vpuv8j20v40943zm.jpg)

进入页面后，在 Repository name 的位置填写域名，格式是 `username.GitHub.io`。

创建成功之后，点击右上角的 Settings，找到 GitHub Pages 选项，选择一个 GitHub 官方提供的主题

![img](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ds2nsvexj20v4021t8m.jpg)

这里我们就随意选择一个主题 Cayman，来看看他的效果是什么样的

![img](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ds2xmpupj20v40ek0ty.jpg)

选择完毕之后 GitHub Pages 就会自动帮你生成好网站，在他跳转的界面点击 Commit changes 按钮，网站就可以访问了。

### 配置自定义域名并免费使用 HTTPS

在 2018 年 5 月 1 日之后，GitHub Pages 已经开始提供免费为自定义域名开启 HTTPS 的功能，并且大大简化了操作的流程，现在用户已经不再需要自己提供证书，只需要将自己的域名使用 CNAME 的方式指向自己的 GitHub Pages 域名即可。

![image-20220521121346853](https://tva1.sinaimg.cn/large/e6c9d24egy1h2fwinyf8mj21qm0rqgqu.jpg)

### 网站生成工具

经历了上面的步骤，现在你的已经有了一个简单的页面了，可是他还远远未满足我们的需求，我们需要利用静态模板系统来让生产接管你博客的文章的生成，让你把更多的经历投入在创作里。下面就 GitHub 官方推荐的 Jekyll 为例子来展开讲讲。

因为 Jekyll 是基于 Ruby 的静态网页生成系统，因此我们首先得安装 Ruby 环境，在 Mac 下我们可以使用的 Homebrew 来进行安装。如果是其他操作系统，可以去参考 [Ruby 官方安装文档](https://www.ruby-lang.org/en/documentation/installation/)进行安装。

```
brew install ruby
```

等 Ruby 安装完毕后再执行以下命令完成 Jekyll 的安装。

```
gem install jekyll bundler
```

采用上面这种方式安装jekyll，报错：

```
Building native extensions. This could take a while...
ERROR: Error installing jekyll:
​	ERROR: Failed to build gem native extension.
  current directory: /Library/Ruby/Gems/2.6.0/gems/eventmachine-1.2.7/ext
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/bin/ruby -I /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0 -r ./siteconf20220519-95417-1vltkqd.rb extconf.rb
checking for -lcrypto... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers. Check the mkmf.log file for more details. You may
need configuration options.
Provided configuration options:
​	--with-opt-dir
​	--without-opt-dir
​	--with-opt-include
​	--without-opt-include=${opt-dir}/include
​	--with-opt-lib
​	--without-opt-lib=${opt-dir}/lib
​	--with-make-prog
​	--without-make-prog
​	--srcdir=.
​	--curdir
​	--ruby=/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/bin/$(RUBY_BASE_NAME)
​	--with-ssl-dir
​	--without-ssl-dir
​	--with-ssl-include
​	--without-ssl-include=${ssl-dir}/include
​	--with-ssl-lib
​	--without-ssl-lib=${ssl-dir}/lib
​	--with-openssl-config
​	--without-openssl-config
​	--with-pkg-config
​	--without-pkg-config
​	--with-cryptolib
​	--without-cryptolib
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:467:in `try_do': The compiler failed to generate an executable file. (RuntimeError)

You have to install development tools first.
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:546:in `block in try_link0'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/tmpdir.rb:93:in `mktmpdir'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:543:in `try_link0'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:570:in `try_link'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:789:in `try_func'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:1016:in `block in have_library'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:959:in `block in checking_for'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:361:in `block (2 levels) in postpone'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:331:in `open'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:361:in `block in postpone'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:331:in `open'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:357:in `postpone'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:958:in `checking_for'
​	from /System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/mkmf.rb:1011:in `have_library'
​	from extconf.rb:8:in `block in check_libs'
​	from extconf.rb:8:in `all?'
​	from extconf.rb:8:in `check_libs'
​	from extconf.rb:95:in `<main>'

To see why this extension failed to compile, please check the mkmf.log which can be found here:
/Library/Ruby/Gems/2.6.0/extensions/universal-darwin-20/2.6.0/eventmachine-1.2.7/mkmf.log
extconf failed, exit code 1
Gem files will remain installed in /Library/Ruby/Gems/2.6.0/gems/eventmachine-1.2.7 for inspection.
Results logged to /Library/Ruby/Gems/2.6.0/extensions/universal-darwin-20/2.6.0/eventmachine-1.2.7/gem_make.out
```

几经周折问题都没有得到解决，后来发现ruby的版本可能是主因

```
(base) wanghaitaodeMacBook-Pro:sealwangdo.github.io Seal$ ruby -v
ruby 2.6.3p62 (2019-04-16 revision 67580) [universal.x86_64-darwin20]
```

使用如下新的方式尝试了下：

### Install chruby and the latest Ruby with ruby-install

Install `chruby` and `ruby-install` with Homebrew:

```
brew install chruby ruby-install
```

Install the latest stable version of Ruby:

```
ruby-install ruby
```

This will take a few minutes, and once it’s done, configure your shell to automatically use `chruby`:

```
echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
echo "chruby ruby-3.1.1" >> ~/.zshrc
```

If you’re using Bash, replace `.zshrc` with `.bash_profile`. If you’re not sure, read this external guide to [find out which shell you’re using](https://www.moncefbelyamani.com/which-shell-am-i-using-how-can-i-switch/).

Quit and relaunch Terminal, then check that everything is working:

```
(base) wanghaitaodeMacBook-Pro:~ Seal$ ruby -v
ruby 3.1.2p20 (2022-04-12 revision 4491bb740a) [x86_64-darwin20]
```

继续

```
sudo gem install jekyll bundler
```

耐心等待结果，否则后面的一切都走不通了......哈哈，成功了，一个石头落地！

```
(base) wanghaitaodeMacBook-Pro:~ Seal$ jekyll -v
jekyll 4.2.2
```

### 制作项目文件

然后进入你 Clone 下来的 GitHub Pages 项目的路径，执行以下命令：

```
jekyll new . --force
```

完成后，Jekyll 会在你指定的目录下生成好所有文件，你可以使用 `bundle exec jekyll serve` 命令

这里又出问题了：

```
(base) wanghaitaodeMacBook-Pro:seal-note Seal$ bundle exec jekyll serve
Configuration file: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note/_config.yml
            Source: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note
       Destination: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.788 seconds.
 Auto-regeneration: enabled for '/Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note'
                    ------------------------------------------------
      Jekyll 4.2.2   Please append `--trace` to the `serve` command 
                     for any additional information or backtrace. 
                    ------------------------------------------------
/Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve/servlet.rb:3:in `<top (required)>'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:179:in `require_relative'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:179:in `setup'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:100:in `process'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `block in process_with_graceful_fail'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `each'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/command.rb:91:in `process_with_graceful_fail'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/lib/jekyll/commands/serve.rb:86:in `block (2 levels) in init_with_program'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `block in execute'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `each'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/command.rb:221:in `execute'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary/program.rb:44:in `go'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/mercenary-0.4.0/lib/mercenary.rb:21:in `program'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/jekyll-4.2.2/exe/jekyll:15:in `<top (required)>'
	from /Users/Seal/.rubies/ruby-3.1.2/bin/jekyll:25:in `load'
	from /Users/Seal/.rubies/ruby-3.1.2/bin/jekyll:25:in `<top (required)>'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli/exec.rb:58:in `load'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli/exec.rb:58:in `kernel_load'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli/exec.rb:23:in `run'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli.rb:483:in `exec'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/vendor/thor/lib/thor/command.rb:27:in `run'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in `invoke_command'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/vendor/thor/lib/thor.rb:392:in `dispatch'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli.rb:31:in `dispatch'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/vendor/thor/lib/thor/base.rb:485:in `start'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/cli.rb:25:in `start'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/exe/bundle:48:in `block in <top (required)>'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/lib/bundler/friendly_errors.rb:103:in `with_friendly_errors'
	from /Users/Seal/.rubies/ruby-3.1.2/lib/ruby/gems/3.1.0/gems/bundler-2.3.14/exe/bundle:36:in `<top (required)>'
	from /Users/Seal/.rubies/ruby-3.1.2/bin/bundle:25:in `load'
	from /Users/Seal/.rubies/ruby-3.1.2/bin/bundle:25:in `<main>'
```

解决方案：

```
bundle add webrick
```

输出信息：

```
(base) wanghaitaodeMacBook-Pro:seal-note Seal$ bundle exec jekyll serve
Configuration file: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note/_config.yml
            Source: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note
       Destination: /Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.401 seconds.
 Auto-regeneration: enabled for '/Users/Seal/Documents/GitHub/sealwangdo.github.io/seal-note'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

然后就可以通过访问 `127.0.0.1:4000` 查看初始界面的样子了。

![img](https://tva1.sinaimg.cn/large/e6c9d24egy1h2ds2r2t80j20v40ohmyb.jpg)



### 更换主题

默认的界面看起来非常的简陋也很丑，但是没关系，你可以在这些网站里根据自己的喜好找到一些美观的主题http://jekyllthemes.org/、https://jekyllthemes.io/、http://themes.jekyllrc.org/。

将主题下载到本地，后执行如下命令：

```
  git clone https://github.com/piharpi/jekyll-klise
  cd jekyll-klise/
  bundle install
  bundle exec jekyll build
  bundle exec jekyll serve
```

效果如下：

![image-20220520114000944](https://tva1.sinaimg.cn/large/e6c9d24egy1h2epx6icqtj21bz0u0mzn.jpg)

主题里的所有关键性配置都在 _config.yml 文件中，你可以根据个人的喜好和不同主题支持的功能来修改具体的内容，这里就不做展开。

到这里完整的搭建的流程已经结束了，你已经可以正常访问你一路配置下来的博客了，接下来你只需要找一个趁手的 Markdown 编辑器来编辑在你本地 GitHub Pages 项目中的 _posts 文件夹里的文章，并使用前面提到的两种方式将文章同步到 GitHub 上即可。需要注意的是，文章的内容和标题需要按照 Jekyll 的格式进行写作。

文章的文件名遵循下面的格式：

```
年-月-日-标题.markdown
```

文章内容顶部必须有下面的 YAML 头信息：

```
---
layout: post
title: Blogging Like a Hacker
---
```



## 尾巴

其实除了 Jekyll 还有非常多的第三方的静态模板系统来搭建 GitHub Pages。比如：

- Node.js 编写的 Hexo
- Go 编写的 Hugo
- Python 编写的 Pelican
- 以及更人性化的 Gridea

他们在各自的基础上实现了更多的功能，比如分析统计、搜索、评论系统、广告、分享系统等。喜欢折腾的同学不妨可以尝试尝试，未来如果有机会希望能更详细的给大家分享一下。