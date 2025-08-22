## use lazy.nvim

```lua
{
  'CopilotC-Nvim/CopilotChat.nvim',
  dependencies = {
    {
      'github/copilot.vim',
      config = function()
        -- vim.keymap.set('i', '<C-g>', 'copilot#Accept()', { silent = true, expr = true, script = true })
        -- vim.keymap.set('i', '<C-g>', '<Plug>(copilot-accept-line)')
        vim.keymap.set('i', '<C-g>', 'copilot#Accept("\\<CR>")', {
          expr = true,
          replace_keycodes = false,
        })
        vim.keymap.set('i', '<C-e>', '<Plug>(copilot-accept-word)')
        vim.g.copilot_no_tab_map = true

        vim.api.nvim_set_keymap('i', '<C-n>', 'copilot#Next()', { silent = true, expr = true, script = true })
        vim.api.nvim_set_keymap('i', '<C-p>', 'copilot#Previous()', { silent = true, expr = true, script = true })
        vim.api.nvim_set_keymap('i', '<C-x>', 'copilot#Clear()', { silent = true, expr = true, script = true })

        -- Optionally, disable Copilot suggestions for specific file types
        vim.cmd [[
  let g:copilot_filetypes = {
    \ 'dotenv': v:false,
    \ 'markdown': v:false,
    \ }
  ]]
      end,
    },
    { 'nvim-lua/plenary.nvim', branch = 'master' }, -- for curl, log and async functions
  },
  -- build = 'make tiktoken', -- Only on MacOS or Linux
  opts = {
    -- See Configuration section for options
  },
  -- See Commands section for default commands if you want to lazy load on them
},
```

> [!IMPORTANT]
> if using termux execute this :

```sh
export XDG_RUNTIME_DIR=$PREFIX/tmp
chmod 777 $PREFIX/tmp
```

> add export to your config

