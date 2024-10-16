# Get Previous Workflow Run Status Action

This action retrieves the status of the previous workflow run for the current workflow.

## Inputs

`GITHUB_TOKEN`: (Optional) The GitHub token for authentication. If not provided, the action will use the default token `${{ github.token }}`.

## Outputs

`last_run_id`: The ID of the last completed workflow run.

`last_run_status`: The conclusion status of the last completed workflow run.

## Example Usage

```yaml
name: CI

on:
  push:

permissions:
  actions: read
  contents: read

jobs:
  get_previous_status:
    runs-on: ubuntu-latest
    steps:
      - name: Do something
        # Here is something your workflow do

      - name: Get previous workflow status
        id: get_last_status
        uses: adel-s/get-last-workflow-run-info@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # Optional, default is ${{ github.token }}

      - name: Display last run details
        run: |
          echo "Last run ID: ${{ steps.get_last_status.outputs.last_run_id }}"
          echo "Last run status: ${{ steps.get_last_status.outputs.last_run_status }}"

      - name: Perform action only if status differs
        if: ${{ steps.get_last_status.outputs.last_run_status != job.status }}
        run: |
          echo "Previous run status differs from current run status."
          # Add your desired action here
```

## Development
I appreciate your interest in contributing to this project. However, I generally do not accept pull requests as I prefer to maintain control over the codebase. 
If you discover any bugs or have feature requests, please feel free to open an issue. I will do my best to address any concerns promptly.

## License
This project is licensed under the [GNU GPLv3 LICENSE](./LICENSE)
