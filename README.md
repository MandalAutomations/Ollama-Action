# Ollama-Action
[![Test](https://github.com/evanallen13/Ollama-Action/actions/workflows/test.yml/badge.svg)](https://github.com/evanallen13/Ollama-Action/actions/workflows/test.yml)
A GitHub composite action that installs [Ollama](https://ollama.com), pulls a model, and runs a prompt — all within your workflow.

## Usage

```yaml
- name: Run Ollama
  uses: evanallen13/Ollama-Action@main
  with:
    model: 'llama3'
    prompt: 'Explain GitHub Actions in one sentence.'
```

## Inputs

| Input    | Description                                      | Required | Default  |
|----------|--------------------------------------------------|----------|----------|
| `model`  | The Ollama model to use (e.g. `llama3`, `mistral`, `gemma`) | Yes | `llama3` |
| `prompt` | The prompt to send to the model                  | Yes      | —        |

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
        uses: evanallen13/Ollama-Action@main
        with:
          model: 'llama3'
          prompt: 'What is the capital of France?'

      - name: Print response
        run: echo "${{ steps.ollama.outputs.response }}"
```
