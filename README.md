# Ollama-Action
[![Test](https://github.com/MandalAutomations/Ollama-Action/actions/workflows/test.yml/badge.svg)](https://github.com/MandalAutomations/Ollama-Action/actions/workflows/test.yml)[![Release date](https://img.shields.io/github/release-date/MandalAutomations/Ollama-Action)](https://packagist.org/MandalAutomations/Ollama-Action)

A GitHub composite action that installs [Ollama](https://ollama.com), pulls a model, and runs a prompt — all within your workflow.

## Usage

```yaml
- name: Run Ollama
  uses: MandalAutomations/Ollama-Action@main
  with:
    model: 'tinyllama'
    prompt: 'Explain GitHub Actions in one sentence.'
```

## Inputs

| Input    | Description                                      | Required | Default      |
|----------|--------------------------------------------------|----------|--------------|
| `model`  | The Ollama model to use (e.g. `tinyllama`, `llama3`, `mistral`) | No | `tinyllama` |
| `prompt` | The prompt to send to the model                  | No       | —            |
| `cache`  | Whether to cache the model between runs (`true`/`false`) | No | `false`  |

## Outputs

| Output     | Description                    |
|------------|--------------------------------|
| `response` | The response from the model    |

## Example Workflow

```yaml
name: Ask Ollama

on:
  workflow_dispatch:

jobs:
  ask:
    runs-on: ubuntu-latest
    steps:
      - name: Run Ollama prompt
        id: ollama
        uses: MandalAutomations/Ollama-Action@main
        with:
          model: 'tinyllama'
          prompt: 'What is the capital of France?'

      - name: Print response
        run: echo "${{ steps.ollama.outputs.response }}"
```
