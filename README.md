# github-script-land-dependabot

This module is to auto-merge dependabot PRs using [github-script](https://github.com/actions/github-script).

## Usage

```yml
...
  automerge:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - uses: actions/setup-node@v1
        with:
          node-version: '12'

      - run: npm i github-script-land-dependabot

      - name: Dependabot Auto Merge
        uses: actions/github-script@v3
        if: ${{ github.actor == 'dependabot[bot]' && github.event_name == 'pull_request' }}
        with:
          github-token: ${{secrets.github_token}}
          script: |
            const automerge = require('github-script-land-dependabot')
            automerge({ github, context })
...
```
