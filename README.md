# notes

## Dependencies

1. [uv](https://docs.astral.sh/uv/getting-started/installation/)
2. Python 3.14: `uv python install 3.12`

## Environment

### VS Code settings.json

```json
{
  "[python]": {
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.fixAll": "explicit",
      "source.organizeImports": "explicit",
    },
    "editor.defaultFormatter": "charliermarsh.ruff",
  }
}
```