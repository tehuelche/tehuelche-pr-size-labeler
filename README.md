
# Pull Request size labeler


## Usage

Create a file named `labeler.yml` inside the `.github/workflows` directory and paste the following configuration.

☝️ Here you can see the default values of all available configuration parameters, however, the only required parameter is the `GITHUB_TOKEN` one.

```yml
name: labeler

on: [pull_request]

jobs:
  labeler:
    runs-on: ubuntu-latest
    name: Label the PR size
    steps:
      - uses: tehuelche/tehuelche-pr-size-labeler@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          message_if_xl: >
            'This PR exceeds the recommended size of 1000 lines.
            Please make sure you are NOT addressing multiple issues with one PR.
            Note this PR might be rejected due to its size.’
          github_api_url: 'api.github.com'
```

## Available parameters

- `*_max_size` (`xs_max_size`, `s_max_size`…): Adjust which amount of changes you consider appropriate for each size based on your project context
- `fail_if_xl`: Set to `'true'` will report GitHub Workflow failure if the PR size is xl allowing to forbid PR merge
- `github_api_url`: Override this parameter in order to use with your own GitHub Enterprise Server. Example: `'github.example.com/api/v3'`

## Basic concepts or assumptions

- PR size labeler consider as a change any kind of line addition, deletion, or modification
- A PR will be labeled as `xl` if it exceeds the amount of changes defined as `l_max_size`

## License

[MIT](LICENSE)
