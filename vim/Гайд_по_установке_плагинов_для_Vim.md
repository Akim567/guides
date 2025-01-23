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

# Плагин `nvim-cmp`

**`nvim-cmp`** — это плагин для автодополнения в Neovim, поддерживающий множество источников, таких как LSP, буфер, путь, командная строка и многое другое. Ниже приведены шаги для установки и настройки.

## 1. Установка

Для установки `nvim-cmp` через менеджер плагинов `lazy.nvim` добавьте следующий код в конфигурацию `lazy.nvim`:

```lua
{
    'hrsh7th/nvim-cmp',
    dependencies = {
        'hrsh7th/cmp-nvim-lsp', -- Поддержка LSP
        'hrsh7th/cmp-buffer',   -- Источник из текущего буфера
        'hrsh7th/cmp-path',     -- Источник файловой системы
        'hrsh7th/cmp-cmdline',  -- Источник командной строки
        'saadparwaiz1/cmp_luasnip', -- Интеграция со snippets через luasnip
        'L3MON4D3/LuaSnip',     -- Плагин для snippets
    },
    config = function()
        local cmp = require('cmp')

        vim.opt.completeopt = { "menu", "menuone", "noselect" } -- Настройка меню автодополнения

        cmp.setup({
            snippet = {
                expand = function(args)
                    require('luasnip').lsp_expand(args.body) -- Поддержка luasnip
                end,
            },
            mapping = cmp.mapping.preset.insert({
                ['<Tab>'] = cmp.mapping.select_next_item(), -- Переключение вперёд
                ['<S-Tab>'] = cmp.mapping.select_prev_item(), -- Переключение назад
                ['<C-b>'] = cmp.mapping.scroll_docs(-4), -- Прокрутка документации вверх
                ['<C-f>'] = cmp.mapping.scroll_docs(4), -- Прокрутка документации вниз
                ['<C-Space>'] = cmp.mapping.complete(), -- Вызов меню автодополнения
                ['<C-e>'] = cmp.mapping.abort(), -- Закрытие меню
                ['<CR>'] = cmp.mapping.confirm({ select = true }), -- Подтверждение выбора
            }),
            sources = cmp.config.sources({
                { name = 'nvim_lsp' }, -- Источник LSP
                { name = 'luasnip' },  -- Источник snippets
                { name = 'buffer' },   -- Источник буфера
                { name = 'path' },     -- Источник файловой системы
            }),
        })

        -- Настройка автодополнения для командной строки
        cmp.setup.cmdline(':', {
            mapping = cmp.mapping.preset.cmdline(),
            sources = cmp.config.sources({
                { name = 'path' },
                { name = 'cmdline' },
            }),
        })
    end,
},
```

---

## 2. Настройка

- Убедитесь, что вы добавили все зависимости для работы с различными источниками:
  - **LSP**: `cmp-nvim-lsp`
  - **Buffer**: `cmp-buffer`
  - **Path**: `cmp-path`
  - **Command Line**: `cmp-cmdline`
  - **Snippets**: `LuaSnip`

- Установите зависимости через `lazy.nvim`:
  ```vim
  :Lazy sync
  ```

---

## 3. Пример использования

- После настройки плагин автоматически активирует автодополнение для LSP, буфера, пути и других источников.
- Вы можете использовать горячие клавиши:
  - `<Tab>` для переключения вперёд.
  - `<S-Tab>` для переключения назад.
  - `<C-Space>` для вызова меню автодополнения.
  - `<CR>` для подтверждения выбора.

---

## 4. Документация

Подробная документация доступна в официальном репозитории `nvim-cmp` на GitHub:

🔗 [hrsh7th/nvim-cmp GitHub](https://github.com/hrsh7th/nvim-cmp)
 

 Итоговый код будет выгдядеть так:  
 ```lua
 local M = {
	"hrsh7th/nvim-cmp",
	dependencies = {
		"hrsh7th/cmp-nvim-lsp",
		"hrsh7th/cmp-nvim-lua",
		"hrsh7th/cmp-buffer",
		"hrsh7th/cmp-path",
		"hrsh7th/cmp-cmdline",
		"saadparwaiz1/cmp_luasnip",
		"L3MON4D3/LuaSnip",
	},
}

M.config = function()
	local cmp = require("cmp")
	vim.opt.completeopt = { "menu", "menuone", "noselect" }

	cmp.setup({
		snippet = {
			expand = function(args)
				require("luasnip").lsp_expand(args.body) -- For `luasnip` users.
			end,
		},
		window = {
			-- completion = cmp.config.window.bordered(),
			-- documentation = cmp.config.window.bordered(),
		},
		mapping = cmp.mapping.preset.insert({
			["<Tab>"] = cmp.mapping.select_next_item(),
			["<S-Tab>"] = cmp.mapping.select_prev_item(),
			["<C-b>"] = cmp.mapping.scroll_docs(-4),
			["<C-f>"] = cmp.mapping.scroll_docs(4),
			["<C-Space>"] = cmp.mapping.complete(),
			["<C-e>"] = cmp.mapping.abort(),
			["<CR>"] = cmp.mapping.confirm({ select = true }), -- Accept currently selected item. Set `select` to `false` to only confirm explicitly selected items.
		}),
		sources = cmp.config.sources({
			{ name = "nvim_lsp" },
			{ name = "nvim_lua" },
			{ name = "luasnip" }, -- For luasnip users.
			-- { name = "orgmode" },
		}, {
			{ name = "buffer" },
			{ name = "path" },
		}),
	})

	cmp.setup.cmdline(":", {
		mapping = cmp.mapping.preset.cmdline(),
		sources = cmp.config.sources({
			{ name = "path" },
		}, {
			{ name = "cmdline" },
		}),
	})
end

return M
```

# Плигин `Mason`
Подробная документация доступна в официальном репозитории на GitHub:  
[Документация](https://github.com/williamboman/mason.nvim?tab=readme-ov-file)  

`Installation`
```lua
{
    "williamboman/mason.nvim"
}
```

`Set up`
```lua
require("mason").setup()
```

```lua
:Mason - команда для просмотра серверов
```

Для установки выбранного серевера нажать i  
