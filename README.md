# Merge coverage reports GitHub Action

GitHub Action to merge coverage reports from parallelized test runners into a single report. 

## Inputs

- `source`*: Path to source code (usually `${{ github.workspace }}`)
- `coverage-reports`*: Path to coverage reports (usually `${{ github.workspace }}/coverage`)
- `output-folder`*: Where to output merged reports

*Required field

## Outputs

- `report`: Full coverage report
- `json-summary`: JSON coverage summary

## Usage

```yaml
  - name: Merge coverage reports
    id: coverage
    uses: aleccool213/merge-coverage@v1.1.4
    with:
      source: ${{ github.workspace }}/${{ inputs.package }}
      coverage-reports: ${{ github.workspace }}/${{ inputs.package }}/coverage
      output-folder: ${{ github.workspace }}/${{ inputs.package }}/coverage-reports
```