# Dota 2 Building Helper - Reborn

[README - English Version](https://github.com/stephenfournier/Dota-2-Building-Helper/blob/master/README.md)

经过一系列的更新之后，V社终于提供了对于客户端粒子特效的支持，现在BuildingHelper也为Panorama进行了完整更新，现在将能够显示建筑物的模型和网格效果，同时提供所有你所需要的建造和建筑物管理的核心特性。

## 包含

#### 核心特性

* 包含建筑网格预览的建造方式
* 为每个建造者储存各自的建造队列
* 加入了额外的建造资源（木材）
* 停止当前建筑，继续建造建筑队列
* 多种建造方式：建筑物自行建造(UD)、工人在建筑内部建造(ORC)，修理方式建造(HUM)，消耗工人方式(ELF)
* 修理的建造方式，提供对于多个工人同时建造同一个建筑的支持
* 支持左右键点击的按键响应和队列

#### 科技树、建造队列、还有更多！

在建造队列之外，你也可以在这个库中找到在RTS和TD类游戏中很常见的特性——科技树，他能够解锁不同的升级、研究之后自动地允许对应建筑的建造。

无论何种时候，当一个建筑开始释放一个持续施法的研究之后，将会使用物品来储存队列，因此不需要额外的UI，只需要每个技能制作一个对应的物品，来让研究队列可以取消就可以了。

**注意** 以下两个系统并没有包括在基础的库中：
- 单位生产
- 金矿/木材收集

如果你对这两个特性这个感兴趣的话，你可以查看[DotaCraft项目](https://github.com/MNoya/DotaCraft)

## 如何为你的游戏模式添加BuildingHelper

有两种不同的方式来使用这个库。
首先，[点击这个链接下载最新的发布版本](https://github.com/stephenfournier/Dota-2-Building-Helper/releases)，你可以进入`samplerts`游戏模式来查看这个特性，你也可以把这个库放到你已经创建的游戏模式中去，下面我将说明一下你所需要移动的文件和进行的设定。

### 如何启动SampleRTS模式
1. 复制整个`content`和`game`文件夹到你的dota文件夹`\Steam\SteamApps\common\dota 2 beta\`。
2. 启动Dota 2 Reborn Tools，你将会在你的addons列表中看到`samplerts`项目。
3. 启动`samplerts`地图，你可以从hammer中启动，也可以在控制台使用这个命令`dota_launch_custom_game samplerts samplerts`来启动

### 如何将BuildingHelper添加到你的游戏模式

你需要做以下这些操作来为你自己的游戏模式添加BuildingHelper

1. Panorama部分
  - 复制`content\dota_addons\samplerts\panorama`文件夹到你自己的panorama文件目录
  - 如果你已经创建了`<custom_ui_manifest.xml>`，那么将下面几行添加到你的`<custom_ui_manifest.xml>`文件的对应位置
  ```
   <CustomUIElement type="Hud" 	layoutfile="file://{resources}/layout/custom_game/scripts.xml" />
   <CustomUIElement type="Hud"  layoutfile="file://{resources}/layout/custom_game/resource.xml" />
   <CustomUIElement type="Hud"  layoutfile="file://{resources}/layout/custom_game/notifications.xml" />
  ```

2. Lua文件
  - 打开`\game\dota_addons\samplerts\scripts\vscripts`文件夹，之后复制所有文件（以下这两个文件**不用**复制）
    - `addon_game_mode.lua` (**但是你需要** 在你自己的addon_game_mode里面添加所有的`require`和`precache`部分)
    - `gamemode.lua` (这个里面包含所有需要的事件和初始化部分的内容)
    - 将所有的`CustomGameMode`改为你自己的游戏模式的类名，(主要是orders.lua和gamemode.lua中的listener和handler部分的内功)

3. KV文件范例
  - BH里面的文件是已经拆分了的，你可以使用 [Dota-2-ModKit](https://github.com/stephenfournier/Dota-2-ModKit)来进行合并，所有必须的技能和技能的范例都在`game\dota_addons\samplerts\scripts\npc`文件夹中了。 
  - 复制 `abilities`, `items` 子文件夹
  -  另外两个文件夹不是必须的(`heroes` 和 `units`) ，但是包含了很重要的键值，之后会解释这个
  
4. 粒子特效
  - 从`game\dota_addons\samplerts\particles`文件夹中复制所有已经编译好的(`vpcf_c`) 文件，当然了，你也可以复制content文件夹中的对应内容

5. 科技树
  - 科技树部分的内容定义在`game\dota_addons\samplerts\scripts\kvtech_tree.kv`这个文件中，复制这个文件到你自己的对应文件夹
  
 

## [使用方法](https://github.com/stephenfournier/Dota-2-Building-Helper/wiki)

### 网格和模型的选项

在 `buildinghelper.lua`中，你可以找到以下几个控制网格和模型的选项

* `GRID_ALPHA`: 定义了在Panorama中建造网格显示的透明度
* `MODEL_ALPHA`: 定义了在Panorama中显示的模型虚像和Lua里面建筑的透明度
* `RECOLOR_GHOST_MODEL`: 是否根据可建造/不可建造对模型进行重新着色
* `RECOLOR_BUILDING_PLACED`: 是否对队列中的建筑进行重新着色
  
## 反馈BUG并提出建议

你可以通过这几个方法找到开发者：

*[在Gtihub上面创建Issue](https://github.com/Myll/Dota-2-Building-Helper/issues/new)
* 通过`irc` --> `irc.gamesurge.net` [#dota2mods & #dota2modhelpdesk](https://kiwiirc.com/client/irc.gamesurge.net/?#dota2mods,#dota2modhelpdesk)
* 通过 [moddota.com](https://moddota.com/forums/), 论坛里面的[工具板块](https://moddota.com/forums/categories/tools)

## 贡献你的代码

贡献你自己的代码是很欢迎的，通过BuildingHelper把DOTA2变为一个适合RTS和TD游戏模式的制作平台需要整个社区的力量。
如果你完成了任何的BUG修复或者你想在这个库里面看到什么新特性，那么你可以发送pull request或者通过issue说明所需要修改的代码。

## 作者

* [Myll](https://github.com/stephenfournier), 原始开发者
* [BMD](https://github.com/bmddota), 研究出如何在Flash里面获取鼠标点击，制作了BH中的粒子特效
* [Perry](https://github.com/perryvw), 贡献了旧的Scaleform版本代码
* [zed](https://github.com/zedor), 贡献了旧的Scaleform版本代码
* [snipplets](https://github.com/snipplets/), Panorama的完成者和队列系统的完成者
* [Noya](https://github.com/MNoya), 发布、更新和维护者

## 提示

如果你是一个新人，那么特别建议你使用[D2ModKit](https://github.com/Myll/Dota-2-ModKit)来fork一个新的项目作为第一个项目。

## 许可

Building Helper 使用的是GNU公开许可证。
