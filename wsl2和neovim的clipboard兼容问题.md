https://www.reddit.com/r/neovim/comments/g94zrl/solution_neovim_clipboard_with_wsl

在init.lua里配置
```lua
  let g:clipboard = {
                \   'name': 'WslClipboard',
                \   'copy': {
                \      '+': 'clip.exe',
                \      '*': 'clip.exe',
                \    },
                \   'paste': {
                \      '+': 'powershell.exe -c [Console]::Out.Write($(Get-Clipboard -Raw).tostring().replace("`r", ""))',
                \      '*': 'powershell.exe -c [Console]::Out.Write($(Get-Clipboard -Raw).tostring().replace("`r", ""))',
                \   },
                \   'cache_enabled': 0,
                \ }
```

在keyoption.lua配置
```lua
opt.clipboard = "unnamedplus"
```
