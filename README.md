# NOTICE

This VS Code extension is far from what it should be. Currently, commits are created file-based. I want a completely different approach.

My priority for now was to get the extension ready to communicate directly with the AI ​​APIs instead of using the VSCode integrated language model settings, which are currently only available in the Insiders version.

Basically, I don't want a file-based approach, but a reconstructive one. AI should take the written source code and logically reconstruct the changes, determining the most likely order in which they were made. Then, using hunks, each change or addition should be added sequentially. This way, with many individual changes, as many consecutive commits as needed would be generated, instead of all changes at once.

For example, changes in two files would ultimately be merged into a single commit if they belong together or are related. Similarly, if a single file contains many unrelated changes, the changes would be split into multiple commits with appropriate messages.


Currently, this extension doesn't quite do what the name Smart Commit Splitter suggests.

However, I would appreciate it if you would star my repository in the meantime.

So stay tuned for some updates on this extension!

# Smart Commit Splitter

Smart Commit Splitter helps you turn a messy working tree into clean, reviewable Git commits without leaving VS Code. It analyzes your current changes, suggests a commit plan, and lets you review it before anything gets written.

## Why this exists

When you work on a feature for a while, your diff usually stops matching the way you actually want to commit it. A small refactor, a fix, a config tweak, and a README change often end up mixed together.

Smart Commit Splitter is built for that exact situation. Instead of dumping everything into one commit, it uses an AI model to propose a logical split with conventional commit messages and a workflow that stays inside the editor.

## Features

- AI-generated commit plans based on the current Git diff.
- Reviewable commit grouping instead of one large catch-all commit.
- Conventional commit style output for cleaner history.
- Sidebar webview with changed files, recent commits, and progress updates.
- Git actions directly from the panel, including staging, unstaging, discarding, and branch switching.
- OpenAI-compatible API support.
- OpenRouter support, including provider-specific headers.
- Hosted OpenRouter model lists with selectable categories.
- Custom JSON URL support for your own hosted model list.

## OpenRouter support

The extension works with OpenRouter and can load curated model lists from hosted JSON files instead of forcing you to type model IDs by hand. It supports built-in source categories for free, budget, standard, and premium programming models, plus a custom JSON URL option for your own list.

The hosted model sources used by the extension are based on this repository:

- [openrouter-model-json](https://github.com/s3tupw1zard/openrouter-model-json)

That makes it easier to keep model selection practical, especially if you want a smaller list focused on coding models instead of the full provider catalog.

## Requirements

- VS Code 1.90 or newer.
- A Git repository opened in your workspace.
- An API key for an OpenAI-compatible provider such as OpenAI or OpenRouter.

## Installation

You can package the extension as a VSIX and install it locally in VS Code.

1. Clone the repository.
2. Install dependencies with `npm install`.
3. Build or package the extension.
4. Install the generated VSIX in VS Code.

## Configuration

The extension uses the `smartCommitSplitter` settings namespace.

### Core settings

- `smartCommitSplitter.baseUrl`: Base URL of your OpenAI-compatible API.
- `smartCommitSplitter.apiKey`: API key for the configured provider.
- `smartCommitSplitter.model`: Model identifier to use for commit planning.
- `smartCommitSplitter.appUrl`: Optional app URL, mainly useful for OpenRouter.
- `smartCommitSplitter.appName`: Optional app name sent to compatible providers.

### OpenRouter settings

- `smartCommitSplitter.openRouterSelectedSource`: Selects the hosted model list source.
- `smartCommitSplitter.openRouterCustomModelListUrl`: Lets you provide your own hosted JSON file.

### Example

```json
{
  "smartCommitSplitter.baseUrl": "https://openrouter.ai/api/v1",
  "smartCommitSplitter.apiKey": "YOUR_API_KEY",
  "smartCommitSplitter.model": "openai/gpt-4o-mini",
  "smartCommitSplitter.appName": "Smart Commit Splitter",
  "smartCommitSplitter.appUrl": "https://github.com/s3tupw1zard/smart-commit-splitter",
  "smartCommitSplitter.openRouterSelectedSource": "programming-budget"
}
```

## Commands

- `Smart Commit Splitter: Split and Commit`
- `Smart Commit Splitter: Select Model`
- `Open Smart Commit Splitter Panel`
- `Refresh`

## Workflow

1. Open a Git repository in VS Code.
2. Make your changes as usual.
3. Open the Smart Commit Splitter panel or run the split command.
4. Let the extension analyze the current diff.
5. Review the generated plan before applying commits.

The idea is simple: keep the convenience of AI assistance, but keep the final decision in your hands.

## Notes

This project is an independent reworked variant and uses its own naming and configuration namespace. The current implementation targets OpenAI-compatible APIs and includes explicit OpenRouter handling, including support for provider headers and curated remote model lists.

## Development

```bash
npm install
npm run compile
```

To test the extension locally, open the project in VS Code and start an Extension Development Host.

## License

MIT
