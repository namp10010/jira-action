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

**The `init` step is always required to setup the jira-cli environment**

A working example can be found in [this workflow](.github/workflows/jira.yml).