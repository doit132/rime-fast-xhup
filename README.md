# Rime 输入法双拼加辅助码方案
<!-- # 这是一个 Rime 配置文件示例 -->
Rime 输入法配置文件，小鹤双拼+自然快手形码辅助方案。使用后打字几乎不需要翻页，且学习成本明显低于五笔等输入方案。

## 方案说明
* 方案名称为“小鹤快手”，它提供了 小鹤双拼+自然快手双形辅助选字 的输入方案，使用 `[` 引出辅助码。
	* 如果希望使用 `Tab` 键也能引出辅助码，可以在 `flypy_zrmfast.custom.yaml` 文件里设置“tab引导辅助码”。默认的 `Tab`，`Shift+Tab` 键功能可以由 `Control+i`，`Control+o` 替代。
	* 如果希望直接输入辅助码而不需要使用符号引导，可以在同样的文件里设置“直接引导辅助码”。
* 允许纯双拼输入。使用形码辅助造词之后，下次可以直接使用双拼部分输入这个词组。
* 例如，输入“输入”这个词组，“输”可以是 `uu`, `uu[i`, `uu[ir`，“入”可以是 `ru`, `ru[p`, `ru[pd`，敲 3×3 种输入码都可以得到“输入”一词。
	* 由于作者只找到了常用字的形码部分码表，有的生僻一些的字没有形码，只能敲其双拼部分来输入。
	* 双形辅助码根据简体字字形给出，即使在繁体输入模式下也是如此。
* 码表基于朙月拼音码表修改得到，保留了对繁体字、含多音字词组的支持特性。小鹤双拼方案通过直接写入码表实现，有能力的用户原则上可以通过自行设置拼写运算修改为全拼/其他双拼方案。
* 自然快手原作者给出的双形辅助码解读（每个字的辅助码是唯一的）：  
![自然快手的辅助码](zrm_fast.jpg)  
根据发音不难记忆。（若需要查某个字的输入码，可以直接在字典文件里搜索，或者利用下方“附加功能”里的 `ab` 前缀。）
* 目前本项目已添加使用小鹤原版辅助码的码表（如涉及侵权，可联系项目作者删除）。如果用户更喜欢小鹤版本的双形，可以在 `flypy_zrmfast.custom.yaml` 文件里设置“使用小鹤原版辅助码”。
	* 在[这个页面](https://xh.flypy.com/#/xyx)的尾部可以看到小鹤的双形拆分规则。另外，本项目只提供单字码，对词组简码有需求的用户建议直接使用官方的小鹤音形输入法。

## 文件说明
* 将这些文件放入 Rime 的用户目录下，重新部署（右键点击任务栏的 Rime 图标）即可。
	* 用户目录：`%APPDATA%\Rime`（Windows），`~/Library/Rime`（MacOS)，`~/.config/ibus/rime`（Linux；根据前端类型，可能需要将 ibus 改成 fcitx 或 fcitx5），`/sdcard/rime`（Android）
	* 如果某些同名文件已经存在，本节的后续部分可能有参考价值。否则，可以直接跳过本节其余内容，去看下一节“附加功能”。
* 一些设置项需要通过修改文件内容实现。Windows（尤其是 7 及以下的版本）自带的记事本可能无法胜任 YAML 文件的编辑任务，推荐使用 Notepad++，VSCode，Sublime Text 等文本编辑器。其他桌面系统的默认文本编辑器原则上都可用。
* `flypy_zrmfast.schema.yaml` 和 `flypy_zrmfast.dict.yaml` 为本方案的主要文件。`flypy_zrmfast.custom.yaml` 提供了一些常用设置项。其余文件均用于附加功能。
* `default.custom.yaml` 仅用于声明本方案的依赖方案。如果用户已经有同名的文件，并且其中设置了 `schema_list` 选项，可以直接将本项目同名文件的内容添加到该选项下，而不必使用项目提供的这一文件。
* `stroke.custom.yaml` 用于初始化“部件组字”功能，部署一次即可生效，后续部署不再必需（除非删除了部署生成的二进制文件）。这个文件会影响五笔画方案（stroke）的默认行为。如果用户已有同名文件，同样将内容添加进去即可，部署一次后可以将添加的内容删除。
* `rime.lua` 文件用于涉及 Lua 的相关功能。如果用户已经有同名的文件，可以将本项目文件的内容复制添加到原有文件之中，但是可能需要自行确认其中的变量名、函数名与原有的那些没有冲突。
* 鉴于部分用户使用的 Rime 版本没有自带 emoji 输入方案，本项目提供了 `emoji.schema.yaml` 和 `emoji.dict.yaml` 文件。如果用户已经有这两个文件，可以不使用本项目提供的版本，不过不排除 emoji 输入时的输入法行为会有所不同。
* `easy_en.schema.yaml` 和 `easy_en.dict.yaml` 为作者基于 [easy-en](https://github.com/BlindingDark/rime-easy-en) 项目的英文输入方案修改得到的版本。如果用户已经有这两个文件，可以不使用本项目提供的版本，但英文单词输入的行为应该会有不同。

## 附加功能
<!-- * 小鹤快手方案、原版小鹤双拼都添加了如下这些奇怪的特性。如无特别说明，以下功能都是在对应的方案文件（`*.schema.yaml`，或 `*.schema.custom.yaml` 里）设置的。 -->
* 置顶字词与自定义词组：由 `custom_phrase.txt` 指定，用户可以根据自己的需要修改和添加。其中，自定义词组使用一些（小鹤双拼下）不对应汉字读音的字母组合作为词组开头，例如 `jf`。
* 鉴于使用辅助码之后很少需要翻页，通常只会用到候选的前几项，方案里设置了分号 `;` 用于输入次选，斜杠 `/` 用于输入第三选项。`flypy_zrmfast.custom.yaml` 里可以设置“单引号用于第3候选”。
* 鉴于双引号比单引号常用，方案里交换了这两个的位置。敲 `'` 输入的是 `“”`，而敲 `"` 输入的是 `‘’`。
	* 如果希望恢复默认的引号输入方式，可以在 `flypy_zrmfast.custom.yaml` 里设置“恢复默认引号”。

### 前缀模式
* `as` 前缀：ASCII 模式，相当于临时切换到西文输入。例如：敲 `ashhh` 空格，即可输入“hhh”。
* 大写字母开头（即敲第一个键的时候按下 `Shift`）：也是 ASCII 模式。例如：敲 `Rime` 空格，即可输入“Rime”。
* `au` 前缀：大写模式，可以输入连续的几个大写字母，不需要大写锁定/`Shift` 键。例如：敲 `aulgpl` 空格，即可输入“LGPL”。
* `aw` 前缀：单词模式，不仅可以敲完整的单词，也允许“简写”，省略掉除了首字母以外的所有元音字母（`aeiou`）。例如：敲 `awelevation` 或者 `awelvtn` 再加空格，即可输入“elevation”。
	* 该功能基于 [easy-en](https://github.com/BlindingDark/rime-easy-en) 项目，简写特性由 `easy_en.schema.yaml` 文件中设置的拼写运算实现。作者对字典文件进行了精简处理以加快部署速度。如果用户希望使用更完整的字典文件，而同时保留简写特性，可以尝试将 `easy_en.dict.yaml` 文件更换为原项目的版本。
	* 使用的一个小 tips：单词第一次输入时用简写，Rime 会将它的词频记录进用户词典。之后的输入只需要敲完整单词的前半部分，它作为输入过的单词就会排在靠前的位置。
* `ae` 前缀：emoji 模式，注意这里需要按照英文输入。例如：敲 `aelaugh` 空格，即可输入“😂”。
* `ap` 前缀：临时全拼模式，用于一些长的词组。例如：敲 `aptlbchqzh` 空格，即可输入“螳螂捕蝉黄雀在后”。
	* 可以设置“使用扩展词典”，例如加入一些常见古诗词，详见 `flypy_zrmfast.custom.yaml` 里的说明。
* `ab` 前缀：部件组字模式（类似搜狗拼音的 u 拆字模式），其中部件按照小鹤双拼输入。例如，要输入“犇”字（它可以拆为“牛牛牛”），敲 `abnqnqnq` 空格即可，并看到这个字的编码是 `bf[nn`。
	* 功能基于 [这篇文章](http://gerry.lamost.org/blog/?p=296003)。一些部件的读音可以参考 [搜狗U模式说明](https://pinyin.sogou.com/help.php?list=3&q=8)（记得要按小鹤双拼输入），此外还有“丶”要敲 `vu`，“廾”要敲 `gs` 等。
	* 如果用户觉得只用笔画比用部件方便，可以在 `flypy_zrmfast.custom.yaml` 中设置“ab前缀改用五笔画输入”（即朙月拼音等输入方案下 `` ` `` 前缀对应的模式），用横竖撇捺折（hspnz，点按捺处理）输入汉字。例如：设置后敲 `abhspn` 空格，即可输入“木”，并看到它的编码是 `mu[ub`。
	* 用户也可以在部件组字模式下同时启用五笔画输入，在 `chaizi_flypy.dict.yaml` 中搜索找到“部件组字模式下启用五笔画”，按要求取消注释即可。不需要修改 `flypy_zrmfast.custom.yaml`。
		* 设置后使用的一个小 tips：一些部件的读音可以用五笔画现查，例如想输入“羿”，先用五笔画敲 `abhps` 查到“廾”的读音为 `gong`（其实查到的是双拼加形方案下的输入码 `gs[hp`、`nm[hp`，读音只看双拼部分，多个读音通常取第一个，也可以都试一遍），于是用部件组字敲 `abyugs` 即可输入“羿”。
* `/` 前缀：符号模式，具体见 Rime 的系统目录自带的 `symbols.yaml` 文件。例如：敲 `/jt` 按 3，即可输入箭头“←”。此外，为避免与候选项选择混淆，用于输入数字相关符号的 `/2`,`/3`,`/4` 分别用 `/er`,`/san`,`/si` 代替。
* `al` 前缀：简易 LaTeX 公式。例如：敲 `al<<f,ff>>ooc0` 空格，即可输入 `$\langle f,\phi\rangle\propto 0$`。
	* 这个功能需要 Lua 支持（下方有简单说明），功能的实现在 `rime.lua` 文件，可以在里面看具体的简写设定，以及试着自己修改（语法应该不难理解）。
	* 目前的简写由重复的字符触发，例如 `aa` 变成 `\alpha`。如果重复的字符是 `jvo` 中的一个，需要接上后面的一个字符触发，例如 `jj;` 变成 `\mapsto`。
	* 形如 `x±1` 的上下标较为常见，用 `oo` 接上 `a/s/d/f`（分别代表：上标+1，上标-1，下标+1，下标-1）中的一个，再接上一个字符即可触发。例如，`xoodn` 会变成 `x_{n+1}`。
	* 使用 `` ` `` 避免重复字符触发，例如敲 `,,bb` 得到 `\math\beta` 不是我们想要的，敲 ``,,b`b`` 则可以得到 `\mathbb`。
	* 如果 `` ` `` 两侧的字符不一样，则变成空格。例如，敲 ``\to`0`` 得到“`\to 0`”
	* 连续的两个 `` ` `` 始终按照一个空格处理。
* 敲 `afd` 可以输入当天的日期。需要 Lua 支持。

### 额外的键位
* 对 Emacs 键位的一些补充
	* `Control+m` 可以替代回车。例如，敲 `yyds` 之后按这个键，输入的就是“yyds”。上面提到过的 `as` 前缀是类似的功能。
	* `Control+w` 可以替代 `Control+退格`，为删一个字的码。例如，敲 `buk` 或者 `buke[dk` 之后，按这个键得到的都是 `bu`，可以继续敲后面的字。如果在词组输入时发现敲错了，可以用这个方式删掉最后的字。
	> Rime 自带的 Emacs 键位包括 `Control+[` 替代 `Esc`，取消当前输入；以及 `Control+h` 替代退格。另外，作者喜欢用 `Control` 键是因为在系统里配置了大写锁定和左 `Control` 交换，这样按起来很舒服。由于这是系统的配置而不是 Rime 的，本文件中没有说明其设置方式。
* 用于追加辅助码的 `Control+1/2/3/4` 快捷键。输入长词组时，如果敲了多个字的双拼部分之后发现需要补充辅助码，此时按 `Control+1` 可以移动光标到第一个音节之后追加辅助码，`Control+2` 可为第二个追加，依此类推。
	* 技术层面而言，该功能依赖 librime 1.6.0 或以上版本；librime 版本在用户目录的 `installation.yaml` 文件中可以看到。若对该功能感兴趣，MacOS 用户将鼠须管升级至最新版本即可，而 Windows 小狼毫和 Android 同文的最新版似乎仍不支持。这种情况下若坚持要使用，可以手动从 [librime 项目](https://github.com/rime/librime/releases) 安装/自行编译。另外，不排除第三方维护的 Rime 前端能支持（未确认），例如 Windows 下的 [PIME](https://github.com/EasyIME/PIME)。
	* 例如，希望输入“适时”一词，敲 `uiui` 发现候选太多，补上最后一个字的形码后 `uiui[oc` 还是没有看到这个词。此时按 `Control+1`，输入框成为 `ui[ 光标 ui[oc`。补充敲下第一个字的形码部分 `q`，然后按 `Control+e`（或者 `End`）把光标移动到最后，即可看到想要的“适时”一词出现在候选中。
	* 禁用这些快捷键的设置稍显复杂，需要在 `flypy_zrmfast.schema.yaml` 里搜索找到 `禁用光标回退补充辅助码快捷键`，按指示注释掉下方 4 行（行首添加 `#` 符号）。
	* 如果希望这些快捷键不要自动补充 `[`，可以找到这 4 行，这次不是注释掉，而是把每行中出现的的 `[` 符号删除。（不过，如果是不小心重复按某个快捷键导致了 `[` 重复，可以使用 `Control+d` 或者 `Delete` 键删除光标后的一个字符）
	* 对于更长的输入码，可以利用 `Control+i`，`Control+o` 移动光标。如果希望自行定义 `Control+5/6/7` 这样的快捷键，也可以找到上面所说的 4 行，在下面照葫芦画瓢追加几行即可。

### 关于 Lua 支持
* 小狼毫（Windows）和鼠须管（MacOS）的最新版本应该都支持 Lua 。
* Trime（Android）要在 [GitHub 页面](https://github.com/osfans/trime) 下载最新测试版（注意不是稳定版）。
* 对于中州韵（Linux），据说 Arch Linux 源提供的 fcitx5-rime 可以在插件设置里开启 Lua 支持。
	* 其他发行版的用户可以考虑这个 [ibus-rime AppImage](https://github.com/hchunhui/build)。遇到调频失效等问题可以试着删除各 userdb、build、sync 文件夹重新部署/同步。如果这一问题反复出现，或者重启/部署/同步之后经常忘掉之前输入的词，可以尝试在 `flypy_zrmfast.custom.yaml` 里开启“用户词典记录为文本格式”，或者看这个 AppImage 有没有发布新版本。
* iRime（iOS）没用过，谁试了或许可以告诉作者（据说这个启用配置文件夹要花钱，而这对使用本项目的配置是必需的）。

## 给进阶用户
这一 Rime 输入方案的制作主要利用了这些文档，希望对 Rime 进行更深入的个性化配置的用户可以参考：
* [GitHub-UserGuide](https://github.com/rime/home/wiki/UserGuide)（访问 GitHub 不稳定的可以用 [Gitee 版 UserGuide](https://gitee.com/lotem/rime-home/wikis/UserGuide)）。其中介绍的 Rime 基本用法适合新手查看，而最开始的“專題”一节还给出了若干有用的链接，供用户在个性化配置时查阅。
	* 其实 UserGuide 只是该项目 wiki 中的一个文件，在网页查看的时候，侧栏里可以看到 wiki 的其他文件，它们也有参考价值。
	* 例如，如果部署后发现没有达到预期的效果，可以考虑从侧栏里点进 `RimeWithSchemata`，按照其中“關於調試”一节下的说明，在日志文件里查找是否有部署出错的提示。
* [设定项详解](https://github.com/LEOYoon-Tsaw/Rime_collections/blob/master/Rime_description.md)。这一文档主要解释了方案文件中各个选项的含义，并且提供了一些配置的例子。

