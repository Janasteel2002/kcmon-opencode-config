# This repo is used to store opencode config files
This config is my personal preference, you can use it as a reference or use it directly.

## How to use

1. Clone this repo
2. Copy the files from .config/opencode/* to your opencode config directory
3. Run opencode

Example:
```bash
cp -r .config/opencode/* ~/.config/opencode/
opencode
```
Example config folder:
![Config folder](/Screenshoot/config-folder-linux.png)

## Orchestration oh-my-opencode config

There are two preset config for oh-my-opencode Agent/Skills Orchestration:

1. [Full Gemini](/.config/opencode/oh-my-opencode-full-gemini.json)
2. [Full Claude](/.config/opencode/oh-my-opencode-full-claude.json)

You can copy the config content and replace oh-my-opencode.json content in your opencode config directory.

## Antigravity auth config

[Antigravity auth config](/.config/opencode/antigravity.json) is my personal preference, you can use it as a reference, use it directly or modify it as per your needs.

You can customize it based on this [schema](https://raw.githubusercontent.com/NoeFabris/opencode-antigravity-auth/main/assets/antigravity.schema.json).