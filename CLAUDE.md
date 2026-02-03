# Claude_Knowledge - Central Knowledge Base

[![GitHub](https://img.shields.io/badge/GitHub-Claude__Knowledge-green?logo=github)](https://github.com/PeckaMilan/Claude_Knowledge)
[![Workflow](https://img.shields.io/badge/Workflow-Claude__Max-blue?logo=github)](https://github.com/PeckaMilan/Claude_Max)

## Purpose

Centrální úložiště znalostí pro všechny Claude projekty. Všechny zjištění, patterny, řešení a best practices se ukládají zde a jsou sdíleny mezi projekty.

## Structure

```
knowledge/
├── domains/        # Business domain knowledge
├── technologies/   # Tech stack knowledge (Python, React, GCP...)
├── patterns/       # Code patterns & architectures
├── errors/         # Error → Solution database
├── apis/           # External API documentation
├── architecture/   # Architecture decisions (ADRs)
└── projects/       # Project-specific learnings
```

## How It Works

1. **Claude discovers** something useful during development
2. **Validates** with Gemini (optional)
3. **Commits** to this repo
4. **Other projects** can read from this repo

## Usage from Other Projects

```bash
# Read knowledge
cat /c/Users/mpeck/PycharmProjects/Claude_Knowledge/knowledge/errors/[topic].md

# Search knowledge
grep -r "search term" /c/Users/mpeck/PycharmProjects/Claude_Knowledge/knowledge/

# Add knowledge (via git)
cd /c/Users/mpeck/PycharmProjects/Claude_Knowledge
# ... add file ...
git add . && git commit -m "knowledge: [topic]" && git push
```

## Entry Format

Each knowledge entry should have:
- Clear title
- Category tags
- Source (which project discovered it)
- Date
- Content
- Examples
- Related entries

## Maintenance

- Auto-indexed daily
- Duplicate detection
- Confidence scoring
- Regular cleanup of outdated entries

## GitHub Repositories

| Repository | Description | URL |
|------------|-------------|-----|
| **Claude_Knowledge** | Central knowledge base (this repo) | https://github.com/PeckaMilan/Claude_Knowledge |
| **Claude_Max** | Workflow toolkit | https://github.com/PeckaMilan/Claude_Max |

### Integration

This knowledge base is integrated with [Claude_Max](https://github.com/PeckaMilan/Claude_Max) workflow via:
- `/ckb` command - search and read knowledge
- `central-kb` skill - automatic knowledge extraction
