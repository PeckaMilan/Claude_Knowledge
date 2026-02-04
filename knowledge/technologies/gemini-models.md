# Gemini AI Models Reference

**Category:** technologies
**Tags:** gemini, google, ai, api, models
**Source:** Claude_Max
**Created:** 2025-02-04
**Confidence:** high

## Summary

Reference for available Google Gemini models via google-genai SDK.

## Current Model (Workflow)

```python
MODEL_NAME = "gemini-3-pro-preview"
```

**Gemini 3 Pro Preview** - nejnovější a nejvýkonnější model pro autonomní development workflow.

## Available Models (February 2025)

### Gemini 3 (Preview)
| Model ID | Name | Use Case |
|----------|------|----------|
| `gemini-3-pro-preview` | Gemini 3 Pro Preview | **Recommended** - Best reasoning |
| `gemini-3-flash-preview` | Gemini 3 Flash Preview | Faster, cheaper |

### Gemini 2.5
| Model ID | Name | Use Case |
|----------|------|----------|
| `gemini-2.5-pro` | Gemini 2.5 Pro | Production stable |
| `gemini-2.5-flash` | Gemini 2.5 Flash | Fast responses |
| `gemini-2.5-flash-lite` | Gemini 2.5 Flash-Lite | Lightweight |

### Gemini 2.0
| Model ID | Name | Use Case |
|----------|------|----------|
| `gemini-2.0-flash` | Gemini 2.0 Flash | Legacy stable |
| `gemini-2.0-flash-lite` | Gemini 2.0 Flash-Lite | Legacy lightweight |

### Specialized
| Model ID | Name | Use Case |
|----------|------|----------|
| `gemini-embedding-001` | Gemini Embedding | Text embeddings |
| `gemini-2.5-flash-native-audio-latest` | Native Audio | Audio processing |
| `gemini-2.5-computer-use-preview-10-2025` | Computer Use | UI automation |

## SDK Usage

```python
from google import genai
from google.genai import types

client = genai.Client(api_key=os.getenv("GOOGLE_API_KEY"))

response = client.models.generate_content(
    model="gemini-3-pro-preview",
    contents="Your prompt",
    config=types.GenerateContentConfig(
        system_instruction="System prompt",
        temperature=0.4,
        max_output_tokens=2048
    )
)

print(response.text)
```

## List Available Models

```python
from google import genai
import os

client = genai.Client(api_key=os.getenv("GOOGLE_API_KEY"))
models = client.models.list()

for model in models:
    if 'gemini' in model.name.lower():
        print(f'{model.name} - {model.display_name}')
```

## Model Selection Guide

| Requirement | Recommended Model |
|-------------|-------------------|
| Best reasoning/quality | `gemini-3-pro-preview` |
| Fast responses | `gemini-3-flash-preview` |
| Production stable | `gemini-2.5-pro` |
| Cost optimization | `gemini-2.5-flash-lite` |
| Embeddings | `gemini-embedding-001` |

## Fallback Chain

```python
MODELS = [
    "gemini-3-pro-preview",    # Primary - best quality
    "gemini-3-flash-preview",  # Fallback 1 - fast
    "gemini-2.5-pro",          # Fallback 2 - stable
    "gemini-2.5-flash",        # Fallback 3
]

for model in MODELS:
    try:
        response = client.models.generate_content(model=model, ...)
        break
    except Exception:
        continue
```

## Environment Setup

```bash
# .env file
GOOGLE_API_KEY=your_api_key_here
```

## Related

- [GCP Service Account Auth](gcp-service-account-auth.md)
- [Consult Skill](../../Claude_Max/.claude/skills/consult/SKILL.md)
