# Outline Mirror

> Outline Mirror uses the [Outline API](https://www.getoutline.com/developers) and [GitHub Actions](https://docs.github.com/en/actions) to create free, fully version controlled snapshots of your Outline wiki at scheduled intervals.

# Usage
1. Create a new repository from [this template](https://github.com/new?template_name=outline-mirror&template_owner=zensharp).
2. Add the following repository secrets:

| Name | Secret |
| --- | --- |
| `OUTLINE_INSTANCE_URL` | URL of your outline instance |
| `OUTLINE_API_KEY` | An API key generated from your outline instance |

4. In repository **Settings > Actions > General**, enable "Read and write permissions".
> [!IMPORTANT]  
> If this option is not available, you may need to enable it at the Organization level.

Now, the workflow will be triggered automatically (default is every 4 hours). You can also manually trigger the workflow from the **Actions** tab.

After the workflow runs, your snapshots will be saved to the `mirror/json` and `mirror/markdown` branches.
