# Deployer Branch Filter - GitHub Action

A [GitHub Action](https://github.com/features/actions) that can be used to filter branches mentioned in [Deployer inventory file hosts.yml](https://deployer.org/docs/hosts.html#inventory-file).

## Installation

To use this GitHub Action, you must have access to GitHub Actions. GitHub Actions are currently only available in public beta (you must [apply for access](https://github.com/features/actions)).

You can use this action before [WordPress Deployer Action](https://github.com/rtCamp/action-wordpress-deploy) to filter out the branches with respect to [hosts.yml](https://github.com/rtCamp/github-actions-wordpress-skeleton/blob/master/.github/hosts.yml), it will only allow workflow to proceed for thhe branches (as top level keys) mentioned in yaml file. Here is an example setup of this action:

1. Create a `.github/main.workflow` in your GitHub repo.
2. Add the following code to the `main.workflow` file and commit it to the repo's `master` branch.

```bash
workflow "WordPress Deployer" {
  resolves = ["Deploy"]
  on = "push"
}

action "Deployer branch filter" {
  uses = "rtCamp/action-deployer-branch-filter@master"
}

action "Deploy" {
  needs = ["Deployer branch filter"
  uses  = "rtCamp/action-wordpress-deploy@master"
  secrets = ["SSH_PRIVATE_KEY"]
}
```

3. Whenever you commit, this action will run and filter the branches.

## License

[MIT](LICENSE) © 2019 rtCamp
