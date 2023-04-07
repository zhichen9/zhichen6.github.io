---
title: Neovim安装和配置
date: 2020-7-8 16:46:24
toc: true
tags:
    - mac
    - Linux
    - vim
---

使用 [Neovim](http://neovim.io) 作为我的编辑器。这个文章迁移自语雀，当时写得比较混乱。

<!--more-->

# Installation

为了使用最新的功能，使用的是v0.6.0的[Pre-release](https://github.com/neovim/neovim/releases)版本。


# Vim-plug

在 `~/.config/nvim/init.vim` 中配置Neovim，这里只记录插件配置。我用[Vim-plug](https://github.com/junegunn/vim-plug)管理插件，安装Vim-plug在指定目录下面

{% codeblock lang:bash line_number:false %}
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.config}"/nvim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
{% endcodeblock %}

一般而言，用 lua 写的插件比vimscript效率高一些。这是我的配置文件
<https://github.com/jinyiliu/.config/blob/master/nvim/init.vim>

## joshdick/onedark.vim

Onedark配色方案，有配套的iTerm2的配色以及lightline和airline的配色方案。

## itchyny/lightline.vim

在对比多个不同的状态栏之后我选择了这个，因为这个非常轻量和简单

{% codeblock lang:vimscript line_number:false %}
let g:lightline = {
    \ 'colorscheme': 'onedark',
    \ }

let g:lightline.tabline = {
    \ 'left': [ [ 'tabs' ] ],
    \ 'right': [  ],
    \ }

let g:lightline.tab = {
    \ 'active': [ 'filename', 'modified' ],
    \ 'inactive': [ 'filename', 'modified' ],
    \ }

let g:lightline.seperator = { 'left': '', 'right': '' }
let g:lightline.subseparator = { 'left': '', 'right': '' }

let g:lightline.enable = {
    \ 'statusline': 1,
    \ 'tabline': 1
    \ }
{% endcodeblock %}

## RRethy/vim-iluminate

高亮当前指针所在的word，好用，速度也很快。

{% codeblock lang:vimscript line_number:false %}
let g:Illuminate_ftblacklist = [ 'nerdtree' ]
let g:Illuminate_delay = 0
hi link illuminatedWord Visual
{% endcodeblock %}

## airblace/vim-gitgutter

一个增强git的显示功能的插件，无脑装。

## LunarWatcher/auto-pairs

A maintained fork of jiangmiao/auto-pairs.

## tpopt/vim-commentary
众多注释插件中这个最好用。

## nvim-telescope/telescope.nvim

这是一个文件搜索的插件，之前有用过传统的nerdtree，不是很好用，后来出了新的fzf（Fuzzy Finder）因为有模糊搜索使文件导航变得容易一些，telescope是最新的文件导航插件，界面简洁好看。注意下面几个插件都要装

{% codeblock lang:vimscript line_number:false %}
Plug 'nvim-lua/popup.nvim'
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'
Plug 'nvim-telescope/telescope-fzy-native.nvim'
{% endcodeblock %}

还有一些其它的nvim-telescope出品的插件比如telescope_frecency.nvim等，但它们不是很重要。这样配置一下

{% codeblock lang:vimscript line_number:false %}
local actions = require('telescope.actions')
require('telescope').setup {
    defaults = {
        entry_prefix = "  ",
        prompt_prefix = "► ",
        selection_caret = "► ",
        initial_mode = "insert",
        sorting_strategy = "descending",
        layout_strategy = "horizontal",
        winblend = 10,
        set_env = { ['COLORTERM'] = 'truecolor' },
        color_devicons = true,
        border = {},
        borderchars = { '─', '│', '─', '│', '╭', '╮', '╯', '╰' },
        path_display = {},
        file_previewer = require'telescope.previewers'.vim_buffer_cat.new,
        grep_previewer = require'telescope.previewers'.vim_buffer_vimgrep.new,
        qflist_previewer = require'telescope.previewers'.vim_buffer_qflist.new,

        buffer_previewer_maker = require'telescope.previewers'.buffer_previewer_maker,

        file_sorter =  require('telescope.sorters').get_fuzzy_file,
        file_ignore_patterns = {},
        generic_sorter =  require'telescope.sorters'.get_generic_fuzzy_sorter,
        mappings = {
            i = {
                ["<C-j>"] = actions.move_selection_next,
                ["<C-k>"] = actions.move_selection_previous,
            },
        },
    }
}
{% endcodeblock %}

## neoclide/coc.nvim

Neovim内置的LSP（Language Server Protocal）还不是特别完善，先用着CoC，虽然总有一天内置LSP会超过。用来做代码补全。

可以输入`:checkhealth provider`来查看一些依赖是否正确安装，我只需要python3 provider就可以了（使用`pip`安装）。

### coc-pyright
[coc-python](https://github.com/neoclide/coc-python) 因为不再进行维护，所以官方建议[coc-pyright](https://github.com/fannheyward/coc-pyright)和 [coc-jedi](https://github.com/pappasam/coc-jedi) 进行python语言的诊断。pyright是微软开发的，jedi依赖环境（需要用`conda`安装jedi的环境），所以还是用coc-pyright比较好。但是微软最近开发了一个更快的linter和补全插件叫pylance，收费使用，仅VScode用户可以用。

但是存在一个不是很美观的地方

<div style="text-align:center">
{% asset_img screenshot.png 500 '"" "中间的线有一些突兀"' %}
</div><br/>

去掉这些需要到`.config/nvim/plugged/coc.nvim/autoload/coc/float.vim`把这一行修改了（对应函数create_cursor_float）

{% codeblock lang:vimscript line_number:false %}
   let width = dimension['width']
-  let lines = map(a:lines, {_, s -> s =~# '^—' ? repeat('—', width) : s})
+  let lines = map(a:lines, {_, s -> s =~# '^—' ? repeat(' ', width) : s})
   let config = extend({'lines': lines, 'relative': 'cursor'}, a:config)
   let config = extend(config, dimension)
{% endcodeblock %}

### coc-json
JSON插件，偶尔需要用它。

### coc-vimlsp
Vim脚本语言的language server工具。

### coc-sh
Bash language server工具，但是装的时候有一些问题，所以一般不会装这个。


## 🗑  Other plugs

没有在使用，但是将来可能用到的插件。

### RRethy/vim-hexokinase

这个是显示颜色的一个插件，依赖Go语言，前端码农应该很需要。

{% codeblock lang:vimscript line_number:false %}
set termguicolors
let g:Hexokinase_highlighters = [ 'backgroundfull' ]
{% endcodeblock %}

### nvim-treesitter/nvim-treesitter

语法高亮的插件。安装完成之后需要安装对应的语言包，我的默认配置

{% codeblock lang:vimscript line_number:false %}
lua << EOF
require'nvim-treesitter.configs'.setup {
  ensure_installed = {  "bash", "c", "c_sharp", "cpp", 
                        "fortran", "python",
                        "json", "html", "latex", "lua" },
  highlight = {
    enable = true,
    disable = { "python", "c" },
  },
}
EOF
{% endcodeblock %}

实际效果确实 python 高亮更花里胡哨了，但是整体视觉体验并没有提升，所以我虽然加载了这个插件，但其实并没有用。

### easymotion/vim-easymotion
其中就两个字母的搜索比较常用（easymotion-s2）

{% codeblock lang:vimscript line_number:false %}
nmap ss <Plug>(easymotion-s2)
let g:EasyMotion_smartcase = 1
{% endcodeblock %}

但还有一个影响颜值的[问题](https://github.com/easymotion/vim-easymotion/issues/421)，不过无所谓，这个插件没有也可以，不是特别影响码代码的效率。

<br/>
