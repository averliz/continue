---
title: Prompt files
---

Prompt files allow you to build and use local prompts, and provide a convenient way to test and iterate on prompts before publishing them to the Hub.

:::info
Visit the Hub to [explore prompts](https://hub.continue.dev/explore/prompts) or [create your own](https://hub.continue.dev/new?type=block&blockType=prompts)
:::

## Quick start

Below is a quick example of setting up a prompt file:

1. Create a folder called `.continue/prompts` at the top level of your workspace (or you can use the button in the UI by typing @, selecting "Prompt Files", and selecting "New Prompt File").
2. Add a file called `rails.prompt` to this folder.
3. Write the following contents to `rails.prompt` and save.

```.prompt
name: Rails Project
description: Information about this project
---
Attached is a summary of the current Ruby on Rails application, including the @Gemfile and database schema in @db/schema.rb
```

Now to use this prompt, you can highlight code and use <kbd>cmd/ctrl</kbd> + <kbd>L</kbd> to select it in the Continue sidebar.

Then, type <kbd>/</kbd> and choose the "Rails Project" prompt. You can now ask any question as usual and the LLM will have the information from your .prompt file.

## Format

The format is inspired by [HumanLoops's .prompt file](https://docs.humanloop.com/docs/prompt-file-format), with additional templating to reference files, URLs, and context providers.

:::info
The current state of this format is experimental and subject to change
:::

### Preamble

The "preamble" is everything above the `---` separator, and lets you specify model parameters. It uses YAML syntax and currently supports the following parameters:

- `name` - The display title
- `description` - The description you will see in the dropdown
- `version` - Can be either "1" (for legacy prompt files) or "2" (this is the default and does not need to be set)

If you don't need any of these parameters, you can leave out the preamble and do not need to include the `---` separator.

### Context

Many [context provider](../context-providers.mdx) can be referenced by typing "@" followed by the name of the context provider. The currently supported list is:

- `@terminal` - The contents of the terminal
- `@currentFile` - The currently active file
- `@open` - All open files
- `@os` - Information about the operating system
- `@problems` - Problems reported by the language server in the active file
- `@repo-map` - A map of files in the repository
- `@tree` - A tree view of the repository structure

Or you can directly type URLs and file paths:

- `@https://github.com/continuedev/continue` - The contents of a URL
- `@src/index.ts` - The contents of a file (VS Code only)

All references will be attached as context items, rather than injected directly inline.

## Feedback

If you have ideas about how to improve the `.prompt` file format, please reach out on [Discord](https://discord.gg/NWtdYexhMs).
