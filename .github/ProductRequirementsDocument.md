# 📜 Product Requirements Document (PRD)

## Objective

Transform an unstructured Zettelkasten into a live, semantic knowledge engine. Maintain high-quality metadata, predictable organization, and a consistent publishing layer. Create a system that allows distributed cognition and tactical review at any time.

## Core Features

* **Metadata-Driven Classification**: Use a comprehensive trait system to categorize and filter notes
* **PARA Structure**: Implement Projects, Areas, Resources, Archive organization for operational clarity
* **Template System**: Provide modular, fill-in-the-blank templates for consistent note creation
* **Visibility Control**: Enable selective publishing based on visibility metadata
* **Knowledge Visualization**: Support Mermaid-powered diagrams of knowledge relationships

## User Persona

A high-agency operator using markdown and Dendron as a command console to document, review, and project strategic thought over time. The system serves as both a personal knowledge repository and a platform for developing and sharing insights.

## User Journeys

### Daily Operations

1. User creates a new daily log using the log template
2. System automatically fills in date and basic metadata
3. User records thoughts, observations, and action items
4. System suggests connections to related notes and projects
5. User reviews and updates project statuses

### Project Management

1. User creates a new project note with strategic metadata
2. System applies the project template structure
3. User defines goals, scope, and dependencies
4. System maintains connections to related resources
5. User tracks progress through status updates

### Knowledge Development

1. User captures an initial idea with exploratory metadata
2. System suggests connections to similar concepts
3. User develops the idea through iterative notes
4. System maintains relationship graph for visualization
5. User selects finished ideas for public visibility

## Expected Outcomes

* A curated, clean public-facing layer of selected notes
* A reliable second-brain vault for personal navigation
* Traceability of idea evolution and project execution
* A Copilot that reinforces structure through metadata validation and smart completion

## Success Metrics

1. **Consistency**: >95% of notes have complete metadata
2. **Connectivity**: Average of 3+ connections per note
3. **Accessibility**: <10 second retrieval time for any note
4. **Publishing**: Automatic deployment of public-facing content
5. **Growth**: Sustainable expansion without degradation of organization

## Technical Requirements

See Technical Requirements Document for detailed specifications on:

- Metadata schema implementation
- Template system design
- Publishing pipeline
- Knowledge graph visualization
- Database structure

## Roadmap

### Phase 1: Foundation
- Set up Dendron environment with PARA structure
- Implement note traits schema
- Create core templates
- Configure basic publishing workflow

### Phase 2: Enhancement
- Develop metadata extraction tools
- Implement connection suggestion system
- Create visualization components
- Integrate with external services

### Phase 3: Optimization
- Refine search capabilities
- Enhance publishing features
- Improve visualization techniques
- Implement analytics and monitoring