[![](https://img.shields.io/github/release/cedrickring/golang-action.svg)](https://github.com/cedrickring/golang-action/releases/latest) [![Actions Status](https://wdp9fww0r9.execute-api.us-west-2.amazonaws.com/production/badge/cedrickring/golang-action)](https://wdp9fww0r9.execute-api.us-west-2.amazonaws.com/production/results/cedrickring/golang-action)
# Golang Action

This Action allows you to run Go commands with your code. It will automatically setup your workspace (`~/go/src/github.com/<your-name>/<repo>`) before the command is run.

## How to use

Create a `workflow.yaml` file in `.github/workflows` with the following contents:
```yaml
on: push
name: My cool Action
job:
  checks:
    name: run
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master

    - name: run
      uses: liptanbiswas/golang-action@1.3.1
```


If no args are specified and a `Makefile` is detected, this action will run `make`. Otherwise `go test` and `go build` will be run.
To run a custom command, just use:
```yaml
steps:
- name: Run custom command
  uses: liptanbiswas/golang-action@1.3.1
  with:
    args: make my-target
```

If your repository's `import` name is different from the path on GitHub,
provide the `import` name by adding an environment variable
`IMPORT=import/name`.  This may be useful if you have forked an open
source Go project:
```yaml
steps:
- name: Run with custom import path
  uses: liptanbiswas/golang-action@1.3.1
  env:
    IMPORT: "root/repo"
```


To use Go Modules add `GO111MODULE=on` to the step:
```yaml
steps:
- name: Go Modules
  uses: liptanbiswas/golang-action@1.3.1
  env:
    GO111MODULE: "on"
```


If your go project is not located at the root of the repo you can also specify environment variable `PROJECT_PATH`:
```yaml
steps:
- name: Custom project path
  uses: liptanbiswas/golang-action@1.3.1
  env:
    PROJECT_PATH: "./path/in/my/project"
```

To use a specific golang version (1.10, 1.11, 1.12):
```yaml
steps:
- name: Use Go 1.11
  uses: cedrickring/golang-action/go1.11@1.3.0
```
