Все плагины должны находиться по такому пути /home/akim/.config/nvim/lua/plugins  

# Плагин **Telescope**
[Ссылка](https://github.com/nvim-telescope/telescope.nvim) на репозиторий плагина  

Первое, что нужно для установки этого плагина - это установить утилиту **fzf**-  
```
sudo apt install fzf
```
Также возможно потребуется установить **ripgrep**
```
sudo apt install ripgrep      
```


Код для самой установки **Telescope**  
```lua
return {
    'nvim-telescope/telescope.nvim', tag = '0.1.8',
    dependencies = { 'nvim-lua/plenary.nvim' },
    } 
```

Код для установки keybundings  
```lua
local builtin = require('telescope.builtin')
vim.keymap.set('n', '<leader>ff', builtin.find_files, {})
vim.keymap.set('n', '<leader>fg', builtin.live_grep, {})
vim.keymap.set('n', '<leader>fb', builtin.buffers, {})
vim.keymap.set('n', '<leader>fh', builtin.help_tags, {})
```

Итоговый код будет выглядеть так:  
```lua
return {
    'nvim-telescope/telescope.nvim', tag = '0.1.8',
    dependencies = { 'nvim-lua/plenary.nvim' },
    config = function()
        require('telescope').setup({})
        local builtin = require('telescope.builtin')
        vim.keymap.set('n', '<leader>ff', builtin.find_files, {})
        vim.keymap.set('n', '<leader>fw', builtin.live_grep, {})
        vim.keymap.set('n', '<leader>fb', builtin.buffers, {})
        vim.keymap.set('n', '<leader>fh', builtin.help_tags, {})
    end
}
``` 

# Плагин **Neo-Tree**

[Ссылка](https://github.com/nvim-neo-tree/neo-tree.nvim) на репозиторий плагина 

Miminal quickstart for Lazy  
```lua
{
    "nvim-neo-tree/neo-tree.nvim",
    branch = "v3.x",
    dependencies = {
      "nvim-lua/plenary.nvim",
      "nvim-tree/nvim-web-devicons", -- not strictly required, but recommended
      "MunifTanjim/nui.nvim",
      -- "3rd/image.nvim", -- Optional image support in preview window: See `# Preview Mode` for more information
    }
}
```
После установки запустить  
``` 
:Neotree
```

Для просмотра списка команд нужно нажать ? в дереве

# Плагин Bufferline

[Ссылка](https://github.com/akinsho/bufferline.nvim) на репозиторий плагина 

Конфиг
```lua
-- using lazy.nvim
{'akinsho/bufferline.nvim', version = "*", dependencies = 'nvim-tree/nvim-web-devicons'}
```

Итоговый код файла конфига **Bufferline**
```lua
return {
	{
		'akinsho/bufferline.nvim',
		version = "*",
		dependencies = 'nvim-tree/nvim-web-devicons',
		config = function()
			require('bufferline').setup({})
		end
	}
}
```   

# Плагин **Lualine**

[Ссылка](https://github.com/nvim-lualine/lualine.nvim?tab=readme-ov-file) на репозиторий плагина 

Установка:  
```lua
{
    'nvim-lualine/lualine.nvim',
    dependencies = { 'nvim-tree/nvim-web-devicons' }
}
``` 

Итоговый код (минимальная конфигурация):  
```lua
return {
    'nvim-lualine/lualine.nvim',
    dependencies = {'nvim-tree/nvim-web-devicons'},
    config = function()
        require('lualine').setup({
		optrions = {
			globalstatus = true
			}
		})
    end
}
```

# Плагин *Onedark**

[Ссылка](https://github.com/joshdick/onedark.vim) на репозиторий плагина 

# Плагин **Treesitter**

[Ссылка](https://github.com/nvim-treesitter/nvim-treesitter) на репозиторий плагина 

Установка:  
```lua
return {
    'nvim-treesitter/nvim-treesitter',
    dependencies = { 'nvim-lua/plenary.nvim' },
```

Конфигурация плагина:  
```lua
config = function()
    require('nvim-treesitter.configs').setup {
```

Подсветка синтаксиса:  
```lua
highlight = {
    enable = true,
    custom_captures = {
        additional_vim_regex_highlighting = false,
    },
},
```

Установка языков:  
```lua 
ensure_installed = {
    "bash",
    "c_sharp",
    "xml",
    "json",
    "html",
    "python",
    "rust",
    "markdown",
    "norg",
    "regex",
    "toml",
    "yaml",
    "vim",
    "vimdoc",
    "diff",
},
```

Сворачивание кода:  
```lua
vim.opt.foldmethod = "expr"
vim.opt.foldexpr = "nvim_treesitter#foldexpr()"
```

Итоговый код:
```lua
return {
    'nvim-treesitter/nvim-treesitter',
    dependencies = { 'nvim-lua/plenary.nvim' },
    config = function()
        require('nvim-treesitter.configs').setup {
            highlight = {
                enable = true,
                custom_captures = {
                    additional_vim_regex_highlighting = false,
                },
            },
            ensure_installed = {
                "bash",
                "c_sharp",
                "xml",
                "json",
                "html",
                "python",
                "rust",
                "markdown",
                "norg",
                "regex",
                "toml",
                "yaml",
                "vim",
                "vimdoc",
                "diff",
            },
        }

        vim.opt.foldmethod = "expr"
        vim.opt.foldexpr = "nvim_treesitter#foldexpr()"
        end,
}
```
