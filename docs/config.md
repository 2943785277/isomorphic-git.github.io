---
title: config
sidebar_label: config
---

Read and/or write to the git config files.

If `value` is provided, it writes to the config file. Otherwise it reads from it.

| param                   | type [= default]         | description                                                                                                                                         |
| ----------------------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **fs**, **dir**, gitdir | FSModule, string, string | The filesystem holding the git repo, the [working tree](dir-vs-gitdir.md) directory path, and optionally the [git directory](dir-vs-gitdir.md) path |
| **path**                | string                   | The key of the git config entry.                                                                                                                    |
| value                   | string                   | (Optional) A value to store at that path.                                                                                                           |
| return                  | Promise\<any\>           | Resolves with the config value                                                                                                                      |

*Caveats:*
- Currently only the local `$GIT_DIR/config` file can be read or written. However support for the global `~/.gitconfig` and system `$(prefix)/etc/gitconfig` will be added in the future.
- The current parser is simply a modified INI parser, so it does not support the more exotic features of the git-config file format such as `[include]` and `[includeIf]`.

```js
let repo = {fs, dir: '<@.@>'}

// Write config value
await git.config({
  ...repo,
  path: '<@user.name@>',
  value: '<@Mr. Test@>'
})

// Read config value
let value = await git.config({
  ...repo,
  path: '<@user.name@>'
})
console.log(value)
```