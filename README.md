# Jira Action

A wrapper around [jira-cli](https://github.com/ankitpokhrel/jira-cli) to allow to use it in GitHub Action.

### Setup

For best security practice, it is recommended to use a [personal access token](https://id.atlassian.com/manage-profile/security/api-tokens) and store it as a secret in your repository.

To use `jira-action` in your workflow, add the following steps

```yaml
    steps:
      - uses: actions/checkout@master
      - name: init
        id: init
        uses: namp10010/jira-action@v0.0.1
        with:
          args: 'init --installation cloud --server ${{ secrets.ATLASIN_BASE_URL }} --login ${{ secrets.ATLASIN_USERNAME }} --project "${{ env.JIRA_PROJECT }}" --board "${{ env.JIRA_BOARD}}"'
      - name: comment
        id: comment
        uses: namp10010/jira-action@v0.0.1
        with:
          args: 'issue comment add GHIN-1 --template - "hello world from github actions"'
```

**The `init` step above is always required to setup the jira-cli environment. It will create a temporary configuration that can be used for subsequent commands**

A working example can be found in [this workflow](.github/workflows/jira.yml).

### Commands in jira-cli

Check out [jira-cli commands](https://github.com/ankitpokhrel/jira-cli#commands) for more details.

`jira-cli` commands are mostly interactive, meaning they will ask for user inputs. To make it work in GitHub Action, you will need to use the `--template` flag.

For better debugging, it is recommended that you test your `jira-cli` command locally before using it in the workflow.

