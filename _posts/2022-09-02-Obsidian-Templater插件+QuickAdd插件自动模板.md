---
layout: post
title: Obsidian | Templater插件+QuickAdd插件自动模板
date: 2022-09-02 14:20:17
description: Obsidian Templater插件和QuickAdd插件的安装与使用教程，包括模板创建和自动命名功能
categories: 技术笔记
tags: Obsidian
---
Obsidian黑曜石是一个功能强大的知识管理软件，是一款功能强大的带有关系图谱功能的双向链笔记，它可基于纯文本Markdown文件的本地文件夹上运行。

- Templater插件可以在不同文件夹中调用不同模板，生成新的文件。适合生成工作日报、论文笔记这些格式固定的文档。
- QuickAdd插件可以让Templater插件创建新文档时，以规定的形式对文档进行命名。例如：以日期命名的日记文档。

## 1. 插件安装
- 1. 【设置】，第三方插件。
- 2. 社区插件市场，【浏览】。
- 3. 搜索Templater和QuickAdd并安装，需要科学上网才能搜索到。
- 4. 开启两个插件开关

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052329866.png" title="Obsidian插件安装界面" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">Obsidian插件安装界面</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052346390.png" title="已安装的插件列表" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">已安装的插件列表</div>

## 2.创建模板

创建所需要的模板，这个模板将会在每次创建新文档时被反复调用。以下以工作日报模板为例子。

~~~ markdown
---
创建时间：2023-02-06 08:42
Tags：日报
---
# 一、今日工作

## 关键事项

## 临时工作

# 二、问题与收获

## 问题

## 收获

# 三、明日计划
~~~

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052329525.png" title="工作日报模板示例" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">工作日报模板示例</div>

## 3. 插件设置

### Templater插件设置
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052329468.png" title="Templater插件设置界面" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">Templater插件设置界面</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052330896.png" title="Templater模板文件夹设置" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">Templater模板文件夹设置</div>

设置好之后，每次你在指定的文件夹里面【新建笔记】时，都会自动以模板生成名字为【未命名】的新文件。

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052330638.png" title="使用模板创建新文件" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">使用模板创建新文件</div>

### QuickAdd插件配置

如果不需要在新建笔记时，模板文件自动命名的话。其实就不需要配置QuickAdd这个插件了。QuickAdd插件中的template功能可以自动生成模板并以固定日期格式命名。比较适合写日记或者工作日报周报。

进入QuickAdd插件的设置页面，进行以下设置。

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052330353.png" title="QuickAdd插件设置界面" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">QuickAdd插件设置界面</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052330515.png" title="QuickAdd模板设置" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">QuickAdd模板设置</div>

完成之后，你就可以在主页面按【ctrl+P】进入控制面板，查找【创建日报】，并选择。

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052330960.png" title="使用QuickAdd创建日报" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">使用QuickAdd创建日报</div>

你就会发现在指定文件夹中生成了，以日期为名字的模板文件。

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="https://raw.githubusercontent.com/alanchancl/BlogImg/main/202302052331367.png" title="自动生成的日报文件" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">自动生成的日报文件</div>

## 参考资料
[每日笔记、日程管理、工作复盘——这是我钻研出的 Obsidian 八般武艺 - 少数派 (sspai.com)](https://sspai.com/post/72385)