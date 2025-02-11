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


# Плагин `dressing`

[Ссылка на плагин](https://github.com/stevearc/dressing.nvim)

`Installation`
```lua
{
  'stevearc/dressing.nvim',
  opts = {},
}
```

Итоговый код будет выглядеть так:  
```lua
return {
	{
	'stevearc/dressing.nvim',
	config = function ()
		require('dressing').setup({
			input = {
				win_options = {
					winhighlight = 'Normal:CmpPmenu, FloatBorder:CmpPmenuBorder, CursorLine:PmenuSel, Search:None'CmpPmenu
				},
			}
		})
	end
	}
}
```


# Плагин `todo-comments`

[Ссылка на плагин](https://github.com/folke/todo-comments.nvim)

`Installation`
```lua
{
  "folke/todo-comments.nvim",
  dependencies = { "nvim-lua/plenary.nvim" },
  opts = {
    -- your configuration comes here
    -- or leave it empty to use the default settings
    -- refer to the configuration section below
  }
}
```

## Команды

```
:TodoTelescope — Открыть Telescope для просмотра всех комментариев.
:TodoQuickFix — Открыть комментарии в Quickfix-окне.
:TodoLocList — Открыть комментарии в локальном списке.
]t — Перейти к следующему комментарию.
[t — Перейти к предыдущему комментарию.
``` 

# Плагин `oil.nvim`

`oil.nvim` — это файловый менеджер для Neovim, который позволяет просматривать и работать с файловой системой прямо в буфере. Это удобный инструмент для навигации по папкам и файлам с минималистичным интерфейсом.
[Ссылка на плагин](https://github.com/stevearc/oil.nvim)  
---

## Основные возможности

1. **Навигация по файловой системе**:  
   - Просмотр текущей папки и её содержимого в буфере.  
   - Возможность копирования, перемещения, удаления и переименования файлов.  

2. **Редактирование файлов**:  
   - Открытие файлов для редактирования прямо из списка.  

3. **Поддержка иконок**:  
   - Интеграция с плагинами для отображения иконок, такими как `nvim-web-devicons` или `mini.icons`.  
---

## Установка

Добавьте плагин в ваш менеджер плагинов (например, `lazy.nvim`):  

```lua
return {
    {
        'stevearc/oil.nvim',
        opts = {}, -- Настройки (можно оставить пустыми для использования настроек по умолчанию)
        dependencies = { "nvim-tree/nvim-web-devicons" }, -- Иконки для файлов (опционально)
    },
} 
```

`Открытие файлового менеджера`
```
:Oil
:Oil some/directory - чтобы отерыть конкретную директорию
```


# Плагин `noice.nvim`

`noice.nvim` — это мощный плагин для улучшения интерфейса сообщений в Neovim. Он модернизирует стандартные сообщения, уведомления, ввод команд и другие элементы, делая взаимодействие с Neovim более удобным и визуально приятным.
[Ссылка на плагин](https://github.com/folke/noice.nvim)  
---

## Основные возможности

1. **Улучшенные уведомления**:
   - Плагин интегрируется с `nvim-notify`, чтобы отображать уведомления в красивом всплывающем стиле.

2. **Модернизация интерфейса сообщений**:
   - Заменяет стандартный вывод команд (например, `:messages`) на более компактный и читаемый.

3. **Обработка команд и ввода**:
   - Улучшает взаимодействие с командами и выводом, добавляя больше визуальной обратной связи.

4. **Интеграция с `nui.nvim`**:
   - Использует библиотеку `nui.nvim` для создания кастомных окон и интерфейсов.

5. **Поддержка событий**:
   - Работает с событием `VeryLazy`, что позволяет загружать плагин только при необходимости, улучшая производительность.

---

## Установка

Добавьте плагин в ваш менеджер плагинов (например, `lazy.nvim`):

```lua
return {
    "folke/noice.nvim",
    event = "VeryLazy", -- Загружать плагин только при необходимости
    opts = {
        -- Здесь можно указать настройки
    },
    dependencies = {
        "MunifTanjim/nui.nvim", -- Зависимость для пользовательских интерфейсов
        "rcarriga/nvim-notify", -- Для уведомлений
    },
}
```

# Плагин `neorg`

`neorg` — это мощный инструмент для организации заметок, задач и проектов в формате Neovim. Он предоставляет уникальную экосистему для управления текстом и проектами, с возможностью создания структурированных рабочих пространств и использования встроенных функций, таких как сворачивание, управление директориями, скрытие элементов и многое другое.
[Ссылка на плагин](https://github.com/nvim-neorg/neorg)  
---

## Основные возможности

1. **Управление рабочими пространствами**:
   - Плагин позволяет организовывать заметки в отдельные рабочие пространства (workspaces), храня их в разных директориях.

2. **Скрытие элементов (`concealing`)**:
   - Поддержка скрытия определённых элементов текста для улучшения читаемости.

3. **Сворачивание текста**:
   - Автоматическое управление сворачиванием разделов для упрощения работы с большими файлами.

4. **Интеграция с другими модулями**:
   - `neorg` поддерживает модульную систему, предоставляя базовые модули (`core`) и расширения для улучшения функционала.

5. **Горячие клавиши**:
   - Возможность быстрого переключения между индексом и заметками с использованием настраиваемых ключей.

---

## Установка

Добавьте плагин в ваш менеджер плагинов (например, `lazy.nvim`):

```lua
return {
    'nvim-neorg/neorg',
    lazy = false,
    version = '*',
    config = function()
        require('neorg').setup {
            load = {
                ['core.defaults'] = {}, -- Загрузка базовых модулей
                ['core.concealer'] = { -- Настройки скрытия элементов
                    config = {
                        folds = true, -- Включить сворачивание
                        init_open_folds = 'never', -- Оставить все свёрнутым
                    },
                },
                ['core.dirman'] = { -- Управление директориями
                    config = {
                        workspaces = {
                            notes = '~/notes', -- Папка для заметок
                        },
                        default_workspace = 'notes', -- Рабочее пространство по умолчанию
                    },
                },
            },
        }

        vim.wo.foldlevel = 99 -- Открыть все уровни свёрток
        vim.wo.conceallevel = 2 -- Включить скрытие элементов
    end,
    keys = {
        {"<leader>ind", "<cmd>Neorg index<cr>", desc = "Go to Index"}, -- Быстрый доступ к индексу
    },
}
```


# Плагин `markdown.nvim`

`markdown.nvim` — это плагин для Neovim, который упрощает работу с Markdown-файлами, обеспечивая поддержку рендеринга, интеграцию с `nvim-treesitter` для подсветки синтаксиса и поддержку иконок с использованием `nvim-web-devicons`.

---

## Основные возможности

1. **Рендеринг Markdown**:
   - Отображение отформатированного содержимого Markdown-файлов прямо в Neovim.

2. **Интеграция с `nvim-treesitter`**:
   - Улучшенная подсветка синтаксиса для Markdown-файлов.

3. **Поддержка иконок**:
   - Использование `nvim-web-devicons` для отображения иконок, связанных с Markdown-документами.

4. **Настраиваемость**:
   - Лёгкая интеграция с существующей конфигурацией Neovim через простой вызов `setup`.

---

## Установка

Добавьте следующий код в вашу конфигурацию для менеджера плагинов (например, `lazy.nvim`):

```lua
return {
    {
        'MeanderingProgrammer/markdown.nvim',
        name = 'render-markdown',
        dependencies = { 'nvim-treesitter', 'nvim-tree/nvim-web-devicons' },
        config = function()
            require('render-markdown').setup({})
        end,
    },
}
```

---

## Использование

1. **Открытие Markdown-файлов**:
   - Просто откройте любой файл с расширением `.md`, чтобы автоматически активировать плагин.

2. **Рендеринг Markdown**:
   - Плагин автоматически применяет подсветку синтаксиса и добавляет иконки.

3. **Интеграция с Treesitter**:
   - Убедитесь, что `nvim-treesitter` установлен и настроен для работы с Markdown:
     ```lua
     require('nvim-treesitter.configs').setup({
         ensure_installed = { 'markdown', 'markdown_inline' },
         highlight = { enable = true },
     })
     ```

4. **Иконки для файлов**:
   - Если установлен `nvim-web-devicons`, плагин добавит иконки для файлов Markdown.

---

## Дополнительные команды

Плагин автоматически активируется при открытии Markdown-файлов и не требует дополнительных команд. Для работы с подсветкой Treesitter выполните:

```bash
:TSInstall markdown markdown_inline
```

---

## Ссылки

- [Репозиторий `markdown.nvim`](https://github.com/MeanderingProgrammer/markdown.nvim)
- [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
- [nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons)



# Плагин `lazygit.nvim`

`lazygit.nvim` — это плагин для Neovim, который интегрирует популярный терминальный инструмент [LazyGit](https://github.com/jesseduffield/lazygit) прямо в ваш редактор. Этот плагин позволяет управлять Git-репозиториями, используя мощный интерфейс LazyGit, без необходимости покидать Neovim.

---

## Основные возможности

1. **Интеграция с LazyGit**:
   - Позволяет открывать интерфейс LazyGit прямо из Neovim.

2. **Управление Git-репозиториями**:
   - Поддержка просмотра изменений, истории, выполнения коммитов, переключения веток и других задач, доступных в LazyGit.

3. **Удобные команды**:
   - Несколько команд для различных сценариев использования (например, работа с текущим файлом или фильтрацией изменений).

4. **Простая интеграция с клавишами**:
   - Легко привязывается к горячим клавишам для быстрого вызова LazyGit.

---

## Установка

Добавьте плагин в вашу конфигурацию (например, `lazy.nvim`):

```lua
return {
    "kdheepak/lazygit.nvim",
    cmd = {
        "LazyGit",
        "LazyGitConfig",
        "LazyGitCurrentFile",
        "LazyGitFilter",
        "LazyGitFilterCurrentFile",
    },
    dependencies = {
        "nvim-lua/plenary.nvim",
    },

    keys = {
        {"<leader>lg", "<cmd>LazyGit<cr>", desc = "LazyGit" }
    }
}
```

---

## Использование

После установки плагина `lazygit.nvim`, вы можете использовать следующие команды:

### Основные команды
- `:LazyGit` — Открыть интерфейс LazyGit для текущего Git-репозитория.
- `:LazyGitConfig` — Открыть конфигурацию LazyGit.
- `:LazyGitCurrentFile` — Показать изменения только для текущего файла.
- `:LazyGitFilter` — Открыть LazyGit с фильтром по указанному файлу или директории.
- `:LazyGitFilterCurrentFile` — Открыть LazyGit с фильтром для текущего файла.

### Горячие клавиши
Плагин включает удобную настройку горячих клавиш:
```lua
keys = {
    {"<leader>lg", "<cmd>LazyGit<cr>", desc = "Открыть LazyGit"}
}
```

- Нажмите `<leader>lg` (по умолчанию `<leader>` — это пробел), чтобы быстро открыть интерфейс LazyGit.

---

# Плагин `flash.nvim`

`flash.nvim` — это плагин для Neovim, который улучшает навигацию по тексту, предоставляя возможности быстрого перемещения, поиска и взаимодействия с элементами кода. Этот плагин поддерживает интеграцию с Treesitter для точной навигации и удобен для использования в различных режимах Neovim.

---

## Основные возможности

1. **Быстрая навигация**:
   - Позволяет быстро перемещаться по тексту в разных режимах (`normal`, `visual`, `operator`).

2. **Интеграция с Treesitter**:
   - Использует Treesitter для точной навигации по синтаксическим элементам кода.

3. **Расширенные функции поиска**:
   - Поддержка поиска в режиме командной строки и переключение режима поиска.

4. **Режим удалённого взаимодействия**:
   - Позволяет работать с удалёнными объектами в тексте.

5. **Гибкая настройка**:
   - Лёгкая настройка горячих клавиш и поведения плагина.

---

## Установка

Добавьте плагин в вашу конфигурацию для `lazy.nvim` или другого менеджера плагинов:

```lua
return {
    {
        'folke/flash.nvim',
        opts = {},
        keys = {
            { "s", mode = { "n", "x", "o" }, function() require("flash").jump() end, desc = "Flash" },
            { "S", mode = { "n", "o", "x" }, function() require("flash").treesitter() end, desc = "Flash Treesitter" },
            { "r", mode = { "o" }, function() require("flash").remote() end, desc = "Remote flash" },
            { "R", mode = { "o", "x" }, function() require("flash").treesitter_search() end, desc = "Treesitter Search" },
            { "<c-s>", mode = { "c" }, function() require("flash").toggle() end, desc = "Toggle Flash Search" },
        }
    },
}
```

---

## Использование

После установки плагина вы можете использовать следующие команды и горячие клавиши для навигации и поиска:

### Основные команды

- **Быстрая навигация (Jump)**:
  Нажмите `s` в нормальном, визуальном или операторном режиме, чтобы активировать быстрый поиск и перемещение по тексту.
  
- **Навигация с Treesitter**:
  Нажмите `S` для использования Treesitter и перехода к синтаксическим элементам кода.

- **Удалённое взаимодействие (Remote)**:
  Нажмите `r` в операторном режиме для работы с удалёнными объектами текста.

- **Поиск с Treesitter (Treesitter Search)**:
  Нажмите `R` в операторном или визуальном режиме для выполнения поиска по синтаксическим элементам через Treesitter.

- **Переключение поиска (Toggle Search)**:
  Нажмите `<Ctrl-s>` в командном режиме для переключения поиска.

### Настроенные горячие клавиши

```lua
keys = {
    { "s", mode = { "n", "x", "o" }, function() require("flash").jump() end, desc = "Flash" },
    { "S", mode = { "n", "o", "x" }, function() require("flash").treesitter() end, desc = "Flash Treesitter" },
    { "r", mode = { "o" }, function() require("flash").remote() end, desc = "Remote flash" },
    { "R", mode = { "o", "x" }, function() require("flash").treesitter_search() end, desc = "Treesitter Search" },
    { "<c-s>", mode = { "c" }, function() require("flash").toggle() end, desc = "Toggle Flash Search" },
}
```

---

## Преимущества использования

- **Точная навигация**:
  Интеграция с Treesitter позволяет работать с синтаксическими элементами, а не просто текстом.

- **Гибкость**:
  Плагин поддерживает несколько режимов работы (нормальный, визуальный, операторный и командный).

- **Эффективность**:
  Значительно ускоряет работу с текстом и кодом, особенно в больших файлах.

---

## Примечания

1. **Поддержка Treesitter**:
   Для полной функциональности убедитесь, что `nvim-treesitter` установлен и настроен.

2. **Кастомизация**:
   Вы можете настроить плагин, добавив параметры в `opts` в конфигурации плагина.

---

## Ссылки

- [Репозиторий `flash.nvim`](https://github.com/folke/flash.nvim)
- [Репозиторий `nvim-treesitter`](https://github.com/nvim-treesitter/nvim-treesitter)
