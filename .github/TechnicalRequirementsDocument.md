# ⚙️ Technical Requirements Document

**Editor**: VS Code
**Extension**: [Dendron](https://wiki.dendron.so/)
**Vault Structure**: PARA-based
**File Format**: Markdown with YAML frontmatter
**Tooling**:

* GitHub Copilot Pro
* Dendron for note management and publishing
* Mermaid.js for diagramming
* GitHub Pages or Vercel for static deployment

## Vault Layout

```
zettelkasten/
├── projects/
│   └── analytics.rebuild/
├── areas/
│   └── personal/
├── resources/
│   └── design.systems/
├── archive/
├── meta/
│   ├── traits.schema.json
│   └── templates/
│       ├── log.md
│       ├── project.md
│       ├── idea.md
│       └── debrief.md
```

## Metadata Schema

### Frontmatter Fields

```yaml
type: [idea | project | log | debrief | tool | reference]
status: [draft | active | completed | archived]
priority: [low | medium | high | mission-critical]
zone: [personal | dev | intelligence | street]
ops-role: [strategic | tactical | archival | exploratory]
visibility: [private | internal | public]
mood: [optional]
connections: [optional]
tags: [optional]
created: [auto]
modified: [auto]
```

## Technical Components

### Note Traits Definition

```json
{
  "type": {
    "values": ["idea", "project", "log", "debrief", "tool", "operation", "contact", "reference", "code"],
    "description": "The fundamental nature of the note",
    "required": true
  },
  "status": {
    "values": ["draft", "active", "archived", "completed", "pending", "abandoned"],
    "description": "Current state of this note or related project",
    "required": true
  },
  "priority": {
    "values": ["low", "medium", "high", "mission-critical"],
    "description": "Importance level for attention and action",
    "required": false
  },
  "ops-role": {
    "values": ["strategic", "tactical", "reflective", "archival", "exploratory"],
    "description": "Operational function this note serves",
    "required": false
  },
  "zone": {
    "values": ["personal", "dev", "street", "intelligence", "financial", "health"],
    "description": "Domain or life area this note belongs to",
    "required": true
  },
  "mood": {
    "values": ["inspired", "focused", "scattered", "exhausted", "curious", "frustrated", "confident"],
    "description": "Mental state during note creation",
    "required": false
  },
  "visibility": {
    "values": ["private", "internal", "public"],
    "description": "Publishing scope for this note",
    "required": true
  },
  "connections": {
    "type": "array",
    "description": "Related notes by ID or direct links",
    "required": false
  },
  "tags": {
    "type": "array",
    "description": "Freeform tags for additional categorization",
    "required": false
  },
  "created": {
    "type": "datetime",
    "description": "Creation timestamp",
    "required": true,
    "auto": true
  },
  "modified": {
    "type": "datetime",
    "description": "Last modification timestamp",
    "required": true,
    "auto": true
  }
}
```

## Implementation Requirements

1. **Database Backend**: PostgreSQL via Neon for metadata indexing and querying
2. **Authentication**: Clerk for user authentication (if multi-user)
3. **Version Control**: Git for tracking changes to notes
4. **Publishing Pipeline**: Static site generator with visibility filtering
5. **API Integration**: GitHub API for code snippet synchronization
6. **Visualization**: Mermaid.js for knowledge graph rendering
7. **Search**: Full-text search with metadata filtering capabilities

## Technical Architecture

The Zettelkasten knowledge engine consists of:

1. **Input Layer**: Note parser, classifier, and metadata extractor
2. **Core Processing**: Metadata storage, query engine, and link analyzer
3. **Template Engine**: Template store, selector, and note renderer
4. **Output Layer**: Result formatter, publishing engine, and command center

## Deployment Considerations

1. Store sensitive configuration in environment variables
2. Set up automated backups of the knowledge base
3. Implement versioning for all published content
4. Configure proper caching for performance optimization
5. Set up monitoring for system health and usage analytics