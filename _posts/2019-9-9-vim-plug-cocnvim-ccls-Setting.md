---
layout: post
title: Vim Plug Coc.nvim ccls code completion setting
---

# Vim Plug Coc.nvim

## ccls代码补全

对于MacOs来说，安装ccls非常简单

```bash
brew update
brew install ccls
```

安装完成后，将配置的内容加入到`coc-setting.json`

```json
"languageserver": {
		"ccls": {
				"command": "ccls",
						"filetypes": [
								"c",
								"cpp",
								"objc",
								"objcpp"
				],
				"rootPatterns": [
								".ccls",
								"compile_commands.json",
								".vim/",
								".git/",
								".hg/"
				],
				"initializationOptions": {
						"cache": {
								"directory": "/tmp/ccls"
						}
				}
		}
}
```

然后会发现，在MacOs下对于基本的系统头文件如`stdio.h`或者`unistd.h`没有头文件的补全，这是因为MacOs将这些头文件都封装起来了，使用命令`g++ -E -x c++ - -v < /dev/null`可以看到会有一系列的输出，在输出`#include <...> search starts here:`以及`End of search list.`之间的路径即为头文件路径

将其加入到coc-setting.json中，同时需要添加`-isystem`参数

```json
-isystem
/usr/local/include
-isystem
/Library/Developer/CommandLineTools/usr/bin/../include/c++/v1
-isystem
/Library/Developer/CommandLineTools/usr/lib/clang/11.0.0/include
-isystem
/Library/Developer/CommandLineTools/usr/include
-isystem
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/include
-isystem
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks
```

最后，同时也是最重要的一步，就是将`.ccls`这个文件放在你项目的根部，这样子这个配置文件才能生效

比如你在`~/project`文件夹进行开发，则需要将`.ccls`放置到`~/project`文件夹中