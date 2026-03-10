# jekyll配置记录

用[tale](https://github.com/chesterhow/tale)模板，目前感觉很不错，记录一点jekyll的知识以及tale的配置知识

## 基本操作

- make post: 在`_post`目录下以`YYYY-MM-DD-name-of-post.ext`格式写入文件，一般就是md格式,基本front matter:
    ```
    ---
    layout: post
    title: "The Mystery of the Filler Post"
    author: "Chester"
    tags: Tale
    ---
    ```
    - 默认每页展示5篇，大部分内容都可以在`_config.yml`文件里修改
- manage excerpt: 在front matter里加入`excerpt_separator: <!--more-->`(当然`:`后的内容可以随意修改),然后在需要截取摘要的地方插入`<!--more-->`摘要就会截止在此处(也就是首页显示的文章内容)
- [写作支持格式](https://chesterhow.github.io/tale/2017-03-16/example-content),意外学到了`~~删除线~~`的写法，以及`<ins>underline<ins>`,`<sup/sub>xxx<sup/sub>`实现的上标与下标，markdown比我想象的还要伟大啊。
- 正如之前写的simple tasker，这里的`_layouts`文件可以加入自己的模板，然后以后写作需要时layout信息就可以用自己的模板,请发挥创造力。