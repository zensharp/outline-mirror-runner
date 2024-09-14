# Outline Mirror Runner

> Outline Mirror uses the [Outline API](https://www.getoutline.com/developers) and [GitHub Actions](https://docs.github.com/en/actions) to create free, fully version controlled snapshots of your Outline wiki at scheduled intervals.

# Configuration
## Runner Repository Setup
> [!TIP]
> If you already have a Runner repository, you can skip this section.

1. Create a "Runner" repository from [this template](https://github.com/new?template_name=outline-mirror-runner&template_owner=zensharp). If you plan on using [environments](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-deployments/managing-environments-for-deployment) (recommended), make this repository public.

2. In the Runner repository **Settings > Actions > General**, enable "Read and write permissions".
> [!IMPORTANT]  
> If this option is not available, you may need to enable it at the Organization level.

## Output Repository Setup
1. Create a "Output" repository which will contain the snapshots. It is recommended that the Output repository is private since this is where your snapshots are stored.
1. Use `ssh-keygen` to generate a key pair. Then, copy the contents of the **public** key (`id_ed25519.pub`).

```shell
ssh-keygen -t ed25519 -f ./id_ed25519
```

1. In the Output repository, go to **Settings > Security > Deploy keys** and "Add deploy key". Paste your key, then enable "Allow write access".

2. In the Runner repository, create a new environment under **Settings > Actions > General**. Add the following environment secrets:

| Name | Description | Example |
| --- | --- | --- |
| `OUTLINE_INSTANCE_URL` | URL of your outline instance | `https://getoutline.com` |
| `OUTLINE_API_KEY` | An API key generated from your outline instance | `ol_api_123456` |
| `OUTPUT_REPO_URL` | The SSH url of the Output repository. | `git@github.com:owner/mywiki-mirror.git` |
| `OUTPUT_SSH_KEY` | The private key (`id_ed25519`) generated earlier. |  |

3. In the Runner repository, add the newly created environment to `jobs.deploy_snapshots.strategy.matrix.ENVIRONMENT`.

# Usage
Now, wait for the Runner repository to trigger the workflow (default is every 4 hours). You can also manually trigger the workflow from the Actions tab.

With each run, the workflow will generate a snapshot of your Outline wiki and push it to your Output repository's `main` branch.

You will also find JSON snapshots on the `json` branch in the Output repository.
