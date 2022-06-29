# `nowsecure-sbom-action`

Generate a Mobile SBOM for an application and submit to the Dependency submission API.

**Features**:

- Integrates with GitHub's [Dependency submission API](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/using-the-dependency-submission-api) to display mobile dependencies inside of GitHub Dependabot alerts,
- Run scans for each commit, or periodically;

## User Guide

This action requires a NowSecure Platform license. If you *are not* a NowSecure customer, click [here](https://bit.ly/ns-git-sbom) to sign up for a free trial to get access.

If you *are* an existing NowSecure customer, proceed with the instructions below.

### Prerequisites

- NowSecure Platform token in GitHub secrets,
  1. In NowSecure Platform, go to "Profile & Preferences" to create a token for GitHub,
  2. In GitHub repository settings, click "Secrets" then "New repository secret". Name the secret `NS_TOKEN`;
- Group ID;

### GitHub Marketplace Setup (recommended)

Go to the [GitHub Marketplace](https://github.com/marketplace?type=&verification=&query=NowSecure+Mobile+SBOM+) and click the "NowSecure Mobile SBOM" action, then click "Use latest version" and follow
the annotated workflow.

### Manual Setup

For an _existing_ workflow,

The action must be run on an `ubuntu-latest` GitHub Action runner.

After the application build step run the NowSecure Mobile SBOM action:

```yml
- name: NowSecure upload app
  uses: nowsecure/nowsecure-sbom-action@v1
  timeout-minutes: 60
  with:
    token: ${{ secrets.NS_TOKEN }}
    app_file: $APPLICATION_PATH # REPLACE: The path to an .ipa or .apk
    group_id: $GROUP_ID         # REPLACE: NowSecure Group ID
```

For a _new_ workflow,

Add a new file called `nowsecure-sbom.yml` in your `.github/workflows` folder and review the [example](workflows/nowsecure-sbom.yml).

## License

This project is released under the [MIT License](https://github.com/nowsecure/nowsecure-action/blob/master/LICENSE).

NowSecure Platform, used in this action, has separate [Terms and Conditions](https://www.nowsecure.com/terms-and-conditions/) and requires a valid license to function.
