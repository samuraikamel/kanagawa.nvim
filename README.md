<p align="center">
  <h2 align="center">🌊 KANAGAWA.nvim 🌊</h2>
</p>

<p align="center">
  <img src="kanagawa@2x.png" width="600" >
</p>

<p align="center">NeoVim dark colorscheme inspired by the colors of the famous painting by Katsushika Hokusai.</p>

<p align="center">
  <h2 align="center"><img src="screenshot.png" width=1024></h2>
</p>
<p align="center">
  <h2 align="center"><img alt="Screenshot" src="https://user-images.githubusercontent.com/36300441/159121961-7c72d6c2-0b1b-4775-81c4-b852afd0987d.png" width=1024></h2>
</p>

## Installation

Download with your favorite package manager.

```lua
use "rebelot/kanagawa.nvim"
```

## Requirements

- neovim latest
- truecolor terminal support
- undercurl terminal support (optional)

## Usage

As simple as writing (pasting)

```vim
colorscheme kanagawa
```

```lua
vim.cmd("colorscheme kanagawa")
```

## Plugin Support

- [Cmp](https://github.com/hrsh7th/nvim-cmp)
- [TreeSitter](https://github.com/nvim-treesitter/nvim-treesitter)
- [LSP Diagnostics](https://neovim.io/doc/user/lsp.html)
- [Git Signs](https://github.com/lewis6991/gitsigns.nvim)
- [Telescope](https://github.com/nvim-telescope/telescope.nvim)
- [NvimTree](https://github.com/kyazdani42/nvim-tree.lua)
- [Indent Blankline](https://github.com/lukas-reineke/indent-blankline.nvim)
- [Dashboard](https://github.com/glepnir/dashboard-nvim)
- [Lualine](https://github.com/nvim-lualine/lualine.nvim)
- [FloaTerm](https://github.com/voldikss/vim-floaterm)
- [dap-ui](https://github.com/rcarriga/nvim-dap-ui.git)
- [Notify](https://github.com/rcarriga/nvim-notify.git)

And many others should _"just work"_!

## Configuration

There is no need to call setup if you are ok with the defaults.

```lua
-- Default options:
require('kanagawa').setup({
    undercurl = true,            -- enable undercurls
    commentStyle = { italic = true },
    functionStyle = {},
    keywordStyle = { italic = true},
    statementStyle = { bold = true },
    typeStyle = {},
    transparent = false,         -- do not set background color
    dimInactive = false,         -- dim inactive window `:h hl-NormalNC`
    terminalColors = true,       -- define vim.g.terminal_color_{0,17}
    colors = {                   -- add/modify theme and palette colors
        palette = {}
        theme = { wave = {}, lotus = {}, dragon = {}, all = {} },
    },
    overrides = function(colors) -- add/modify highlights
        return {}
    end,
    theme = "wave"               -- Load "wave" theme when 'background' option is not set
    background = {               -- map the value of 'background' option to a theme
        dark = "wave",           -- try "dragon" !
        light = "lotus"
    },
})

-- setup must be called before loading
vim.cmd("colorscheme kanagawa")
```

## Themes

Kanagawa comes in three variants:

- `wave` the default heart-warming theme,
- `dragon` for those late-night sessions
- `lotus` for when you're out in the open.

Themes can be changed in three ways:

- Setting `config.theme` to the desired theme. Note that `vim.o.background` **must** be unset.
- Using the `background` option:
  Any change to the value of `vim.o.background` will select the theme mapped by `config.background`.
  Use `vim.o.background = ""` to unset this option.
- Loading the colorscheme directly with:
  ```lua
  vim.cmd("colorscheme kanagawa-wave")
  vim.cmd("colorscheme kanagawa-dragon")
  vim.cmd("colorscheme kanagawa-lotus")
  ```
  or
  ```lua
  require("kanagawa").load("wave")
  ```

## Customization

In kanagawa, there are _two_ kinds of colors: `PaletteColors` and `ThemeColors`;
`PaletteColors` are defined directly as RGB Hex strings, and have arbitrary names
that recall their actual color. Conversely, `ThemeColors` are named and grouped _semantically_
on the basis of their actual function.

In short, a `palette` defines all the available colors, while a `theme` maps the `PaletteColors`
to specific `ThemeColors` and the same palette color may be assigned to multiple theme colors.

You can change _both_ theme or palette colors using `config.colors`.
All the palette color names can be found [here](lua/kanagawa/colors.lua),
while their usage by each theme can be found [here](lua/kanagawa/themes.lua).

```lua
require('kanagawa').setup({
    ...,
    colors = {
        palette = {
            -- change all usages of these colors
            sumiInk0 = "#000000",
            fujiWhite = "#FFFFFF",
        },
        theme = {
            -- change specific usages for a certain theme or all of them
            wave = {
                ui = {
                    float = {
                        bg = "none",
                    },
                },
            },
            dragon = {
                syn = {
                    parameter = "yellow",
                },
            }
            all = {
                ui = {
                    bg_gutter = "none"
                }
            }
        }
    },
    ...
})
```

You can also conveniently add/modify `hlgroups` using the `config.overrides` option.
Supported keywords are the same for `:h nvim_set_hl` `{val}` parameter.

```lua
require('kanagawa').setup({
    ...,
    overrides = function(colors)
        return {
            -- Assign a static color to strings
            String = { fg = colors.palette.carpYellow, italic = true },
            -- theme colors will update dynamically when you change theme!
            SomePluginHl = { fg = colors.theme.syn.type, bold = true },
        }
    end,
    ...
})
```

## Integration

```lua
-- Get the colors for the current theme
local colors = require("kanagawa.colors").setup()
local palette_colors = colors.palette
local theme_colors = colors.theme

-- Get the colors for a specific theme
local wave_colors = require("kanagawa.colors").setup({ theme = 'wave' })
```

## Color palette

|                                                         | Name          |    Hex    | Usage                                                                             |
| :-----------------------------------------------------: | :------------ | :-------: | :-------------------------------------------------------------------------------- |
|   <img src="assets/circles/fujiWhite.svg" width="40">   | fujiWhite     | `#DCD7BA` | Default foreground                                                                |
|   <img src="assets/circles/oldWhite.svg" width="40">    | oldWhite      | `#C8C093` | Dark foreground (statuslines)                                                     |
|   <img src="assets/circles/sumiInk0.svg" width="40">    | sumiInk0      | `#16161D` | Dark background (statuslines and floating windows)                                |
|   <img src="assets/circles/sumiInk1.svg" width="40">    | sumiInk1      | `#1F1F28` | Default background                                                                |
|   <img src="assets/circles/sumiInk2.svg" width="40">    | sumiInk2      | `#2A2A37` | Lighter background (colorcolumn, folds)                                           |
|   <img src="assets/circles/sumiInk3.svg" width="40">    | sumiInk3      | `#363646` | Lighter background (cursorline)                                                   |
|   <img src="assets/circles/sumiInk4.svg" width="40">    | sumiInk4      | `#54546D` | Darker foreground (line numbers, fold column, non-text characters), float borders |
|   <img src="assets/circles/waveBlue1.svg" width="40">   | waveBlue1     | `#223249` | Popup background, visual selection background                                     |
|   <img src="assets/circles/waveBlue2.svg" width="40">   | waveBlue2     | `#2D4F67` | Popup selection background, search background                                     |
|  <img src="assets/circles/winterGreen.svg" width="40">  | winterGreen   | `#2B3328` | Diff Add (background)                                                             |
| <img src="assets/circles/winterYellow.svg" width="40">  | winterYellow  | `#49443C` | Diff Change (background)                                                          |
|   <img src="assets/circles/winterRed.svg" width="40">   | winterRed     | `#43242B` | Diff Deleted (background)                                                         |
|  <img src="assets/circles/winterBlue.svg" width="40">   | winterBlue    | `#252535` | Diff Line (background)                                                            |
|  <img src="assets/circles/autumnGreen.svg" width="40">  | autumnGreen   | `#76946A` | Git Add                                                                           |
|   <img src="assets/circles/autumnRed.svg" width="40">   | autumnRed     | `#C34043` | Git Delete                                                                        |
| <img src="assets/circles/autumnYellow.svg" width="40">  | autumnYellow  | `#DCA561` | Git Change                                                                        |
|  <img src="assets/circles/samuraiRed.svg" width="40">   | samuraiRed    | `#E82424` | Diagnostic Error                                                                  |
|  <img src="assets/circles/roninYellow.svg" width="40">  | roninYellow   | `#FF9E3B` | Diagnostic Warning                                                                |
|   <img src="assets/circles/waveAqua1.svg" width="40">   | waveAqua1     | `#6A9589` | Diagnostic Info                                                                   |
|  <img src="assets/circles/dragonBlue.svg" width="40">   | dragonBlue    | `#658594` | Diagnostic Hint                                                                   |
|   <img src="assets/circles/fujiGray.svg" width="40">    | fujiGray      | `#727169` | Comments                                                                          |
| <img src="assets/circles/springViolet1.svg" width="40"> | springViolet1 | `#938AA9` | Light foreground                                                                  |
|   <img src="assets/circles/oniViolet.svg" width="40">   | oniViolet     | `#957FB8` | Statements and Keywords                                                           |
|  <img src="assets/circles/crystalBlue.svg" width="40">  | crystalBlue   | `#7E9CD8` | Functions and Titles                                                              |
| <img src="assets/circles/springViolet2.svg" width="40"> | springViolet2 | `#9CABCA` | Brackets and punctuation                                                          |
|  <img src="assets/circles/springBlue.svg" width="40">   | springBlue    | `#7FB4CA` | Specials and builtin functions                                                    |
|   <img src="assets/circles/lightBlue.svg" width="40">   | lightBlue     | `#A3D4D5` | Not used                                                                          |
|   <img src="assets/circles/waveAqua2.svg" width="40">   | waveAqua2     | `#7AA89F` | Types                                                                             |
|  <img src="assets/circles/springGreen.svg" width="40">  | springGreen   | `#98BB6C` | Strings                                                                           |
|  <img src="assets/circles/boatYellow1.svg" width="40">  | boatYellow1   | `#938056` | Not used                                                                          |
|  <img src="assets/circles/boatYellow2.svg" width="40">  | boatYellow2   | `#C0A36E` | Operators, RegEx                                                                  |
|  <img src="assets/circles/carpYellow.svg" width="40">   | carpYellow    | `#E6C384` | Identifiers                                                                       |
|  <img src="assets/circles/sakuraPink.svg" width="40">   | sakuraPink    | `#D27E99` | Numbers                                                                           |
|    <img src="assets/circles/waveRed.svg" width="40">    | waveRed       | `#E46876` | Standout specials 1 (builtin variables)                                           |
|   <img src="assets/circles/peachRed.svg" width="40">    | peachRed      | `#FF5D62` | Standout specials 2 (exception handling, return)                                  |
| <img src="assets/circles/surimiOrange.svg" width="40">  | surimiOrange  | `#FFA066` | Constants, imports, booleans                                                      |
|  <img src="assets/circles/katanaGray.svg" width="40">   | katanaGray    | `#717C7C` | Deprecated                                                                        |

## Extras

- [alacritty](extras/alacritty_kanagawa.yml)
- [base16](extras/base16-theme.yaml)
- [broot](extras/broot_kanagawa.toml)
- [fish](extras/kanagawa.fish)
- [foot](extras/foot_kanagawa.ini)
- [iTerm](extras/kanagawa.itermcolors)
- [kitty](extras/kanagawa.conf)
- [mintty](extras/kanagawa.minttyrc)
- [pywal](extras/pywal-theme.json)
- [wezterm](extras/wezterm.lua)
- [Windows Terminal](extras/windows_terminal.json)
- [Xresources](extras/.Xresources)
- 🎉 Bonus! You win a tiny [python script](palette.py)🐍 to extract color palettes 🎨 from any image! 🥳

## Acknowledgements

- [Tokyonight](https://github.com/folke/tokyonight.nvim)
- [Gruvbox](https://github.com/morhetz/gruvbox)
- [Affinity Designer](https://affinity.serif.com/designer/)

## Related projects

- [kanagawa.vim](https://github.com/guigui64/kanawaga.vim) - unaffiliated vimscript port of kanagawa.nvim

### Donate

Buy me coffee and support my work ;)

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?business=VNQPHGW4JEM3S&no_recurring=0&item_name=Buy+me+coffee+and+support+my+work+%3B%29&currency_code=EUR)
