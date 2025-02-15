---
id: e3pzpy5r9lz2w9xim4bh43m
title: '043114'
desc: ''
updated: 1739334674094
created: 1739334674094
---

# 📜 Dendron Markdown Specifications

##### A structured guide to the markdown syntax used in the VS Code Dendron extension

___

## 1️⃣ Frontmatter (YAML)

Dendron uses **YAML frontmatter** at the beginning of each note to store metadata.

### Example:

```yaml
---
id: rir7v203jlk3hqrnq8hhhzp  # Unique identifier (auto-generated)
title: '074044'  # Display title in military time format
desc: 'A brief description of the note'  # Note description
updated: 1739199889731  # Last updated timestamp
created: 1739198479074  # Creation timestamp
---
```

### ✅ Rules & Notes:

1. **Mandatory in all notes**
2. **ID must be a unique 23-character alphanumeric string**
3. **Timestamps use Unix Epoch in milliseconds**
4. **Title must be the note creation time in military (hhmmss) format**
5. **Description is optional but recommended**

___

## 2️⃣ Hierarchical Note Organization (HNO)

Dendron **structures notes hierarchically** using `.` as a delimiter.

### ✅ Example Naming Conventions:

- `projects.tech.nextjs` → Note about Next.js under "tech" inside "projects."
- `4-Archive.scratch.2025.02.11.143000` → Archive scratch note (timestamped).

### ✅ Rules & Notes:

1. Notes **must** follow a hierarchy.
2. Each note name should be **unique** within its workspace.
3. Naming **replaces folders**—Dendron organizes notes dynamically.

___

## 3️⃣ Wiki-Style Internal Linking

Dendron uses `[[wikilinks]]` for **internal note references**.

### Examples:

```markdown
See [[projects.tech.nextjs]] for details.
```
Or use **custom text for links**:

```markdown
Learn more about [[projects.tech.nextjs|Next.js Development]].
```

### ✅ Rules & Notes:

- Use `[[note-name]]` instead of `[text](note-name.md)`.
- Supports **relative links** within the hierarchy.

___

## 4️⃣ Tag System

Dendron supports `#tags` for **categorization**.

### Example:

```markdown
#tech #webdev
```

### ✅ Rules & Notes:

1. Tags can be placed **anywhere** in the note.
2. Tags do **not** create new notes—they are just labels.

___

## 5️⃣ Block Anchors & Transclusion

Dendron enables referencing **specific sections** of a note.

### ✅ Block Anchors (Headings as Links)

```markdown
[[projects.tech.nextjs#setup-guide]]
```
This links directly to the `# Setup Guide` section inside `projects.tech.nextjs`.

### ✅ Transclusion (Embedding Notes)

```markdown
![[projects.tech.nextjs]]
```
This **embeds** the contents of `projects.tech.nextjs` inside the current note.

___

## 6️⃣ Special Formatting & Features

### ✅ Callouts

```markdown
> [!note] This is a note.
> [!warning] Be careful with this setting.
```

### ✅ Checkboxes (Task Lists)

```markdown
- [ ] Incomplete Task
- [x] Completed Task
```

### ✅ Code Blocks (Supports syntax highlighting)

```markdown
```javascript
console.log("Hello, Dendron!");
```
```

### ✅ Latex Support (for math formulas)

```markdown
$$E = mc^2$$
```

___

## 🎯 Conclusion

Dendron Markdown is **hierarchical, structured, and optimized** for large-scale note-taking in VS Code. It extends **standard Markdown** with:

1. **YAML Frontmatter** for metadata.
2. **Hierarchical Notes** using `.` notation.
3. **Wiki-Style Links** for navigation.
4. **Tags & Block Anchors** for organization.
5. **Transclusion** for embedded content.
6. **Special Formatting** (callouts, checkboxes, code blocks, LaTeX, etc.).

This format ensures **scalability, organization, and rapid searchability**, making it ideal for **knowledge management** and **documentation**.

