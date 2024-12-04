# Patched GenerateREADME Action

This GitHub Action uses [patchwork-cli](https://docs.patched.codes/patchwork/quickstart) to automatically generate documentation for a folder in your repository in form of a README.md file.

## Features

- Automatically generates documentation from your code
- Supports various LLM providers (OpenAI, local models, or custom endpoints)
- Creates pull requests with the generated documentation
- Configurable file filtering and comment handling
- Customizable output file name and branch naming

## Usage

```yaml
name: Generate Documentation
on:
  workflow_dispatch: # Allow manual triggers

jobs:
  generate-docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: patched-codes/GenerateREADME@0.1.0
        with:
          patched_api_key: ${{ secrets.PATCHED_API_KEY }}
          folder_path: "./src" # Path to the folder to generate documentation for
```

## Inputs

### Required

One of the following must be provided:

- `patched_api_key`: Patched API key for the LLM ([Get an API key](https://app.patched.codes/))
- `openai_api_key`: OpenAI API key for the LLM ([Get an API key](https://platform.openai.com/account/api-keys))

### Optional

- `folder_path`: Path to the folder to generate documentation for (default: './')
- `github_token`: GitHub token for creating pull requests (default: [Automatically set by GitHub](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication))
- `model`: LLM model to use
- `client_base_url`: Base URL for the LLM API
- `filter`: Filter for the kind of files to include (e.g., '\*.py' for Python files)
- `suppress_comments`: Whether to suppress comments in the documentation
- `markdown_file_name`: Name of the generated markdown file
- `branch_prefix`: Prefix for the created branch (default: 'patched-generate-readme/')
- `disable_branch`: Disable creating new branches
- `disable_pr`: Disable creating pull requests
- `force_pr_creation`: Force push commits to existing PR
- `model_temperature`: Temperature parameter for the LLM
- `model_top_p`: Top-p parameter for the LLM
- `model_max_tokens`: Maximum tokens for the LLM response

## Examples

### Basic Usage

```yaml
- uses: patched-codes/GenerateREADME@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
    folder_path: "./src"
```

### Custom Documentation Settings

```yaml
- uses: patched-codes/GenerateREADME@0.1.0
  with:
    patched_api_key: ${{ secrets.PATCHED_API_KEY }}
    folder_path: "./src"
    filter: "*.py"
    suppress_comments: true
    markdown_file_name: "API.md"
```

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
