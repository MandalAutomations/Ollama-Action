# Ollama-Action

A **composite** GitHub Action that installs [Ollama](https://ollama.com), pulls a model, and optionally runs a prompt — all inside your GitHub Actions workflow.

## Inputs

| Input | Description | Required | Default |
|---|---|---|---|
| `model` | Ollama model to pull and use (e.g. `llama3`, `mistral`, `gemma2`) | No | `llama3` |
| `prompt` | Prompt to send to the model | No | _(empty)_ |
| `ollama_version` | Version of Ollama to install (e.g. `v0.3.0`). Leave empty for the latest release. | No | _(latest)_ |

## Outputs

| Output | Description |
|---|---|
| `response` | The model response to the prompt (only set when `prompt` is provided) |

## Usage

### Pull a model only

```yaml
- uses: MandalAutomations/Ollama-Action@v1
  with:
    model: llama3
```

### Pull a model and run a prompt

```yaml
- name: Run Ollama prompt
  id: ollama
  uses: MandalAutomations/Ollama-Action@v1
  with:
    model: llama3
    prompt: 'Explain GitHub Actions in one sentence.'

- name: Print response
  run: echo "${{ steps.ollama.outputs.response }}"
```

### Pin to a specific Ollama version

```yaml
- uses: MandalAutomations/Ollama-Action@v1
  with:
    model: mistral
    prompt: 'What is the capital of France?'
    ollama_version: v0.3.0
```

## Full workflow example

```yaml
name: Ollama Example

on:
  push:
    branches: [main]

jobs:
  ollama:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Ollama
        id: ollama
        uses: MandalAutomations/Ollama-Action@v1
        with:
          model: llama3
          prompt: 'Say hello in three different languages.'

      - name: Print response
        run: echo "${{ steps.ollama.outputs.response }}"
```

## Requirements

- The action currently supports **Linux** runners (`ubuntu-*`).
- The runner must have internet access to reach `ollama.com` for installation and model download.
