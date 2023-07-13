# Merge coverage reports GitHub Action

GitHub Action to merge coverage reports from parallelized test runners into a single report. 

For use with SonarQube. If you need more inputs/outputs, please raise an issue.

## How it works

This Github Action will download unmerged code coverage report folders from an artifact, collect all of the files, merge them, perform some text processing, create a report, and upload it as an artifact.

### Weird nyc report cmd behavior

This action accounts for the workspace directory inside reports needing to be the same as the current workspace for nyc report command. This is needed because nyc report command will not work if the workspace directory is not the same as the directory where the code coverage report was first generated. This is a weird behavior of nyc report command.

ref: https://github.com/istanbuljs/nyc/issues/1249#issuecomment-677928933

## Inputs

- `unmerged-coverage-reports-artifact-name`*: 'Name of the unmerged coverage reports artifact. Should be a folder which contains sub-folders that contain coverage-file.json files.'
- `output-folder`*: 'Folder to output the merged coverage report to. Included in the path of the uploaded artifact. For example, ./code-coverage-data/coverage/lcov.info'
- `code-coverage-workspace-generates`*: The workspace directory of the job which generates the coverage reports. You can obtain this by echoing the github.workspace attribute in the job which generates the coverage reports.
- `merged-code-coverage-artifact-name`*: 'Name of the merged coverage reports artifact which gets uploaded.'

*Required field

## Outputs

nothing

## Usage

```yaml
      - name: Merge coverage reports
        id: coverage
        uses: aleccool213/merge-coverage@v1.2.0
        with:
          source: ${{ github.workspace }}
          unmerged-coverage-reports-artifact-name: unmerged-code-coverage-data
          output-folder: code-coverage-data
          code-coverage-workspace-generates: /runner/_work/example-repo/exmaple-repo
          merged-code-coverage-artifact-name: code-coverage-data
```