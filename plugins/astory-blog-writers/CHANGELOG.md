# Changelog

All notable changes to the astory-blog-writers plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-01-06

### Added

#### Hybrid Author System

- Complete DNA-based persona system with 16 atomic traits
- Trait categories: Voice (4), Expertise (4), Perspective (4), Tone (4)
- 256+ possible persona combinations through DNA mixing

#### Writing Modes

- **Solo Mode**: Single persona for fast, consistent writing
- **Crew Mode**: 7-role collaboration for highest quality content
- **Adaptive Mode**: Automatic persona switching per section

#### Crew Collaboration System

- Creative Director: Ideation and angle discovery
- Research Analyst: Deep research and source gathering
- Lead Writer: Primary content drafting
- Technical Reviewer: Accuracy verification
- Reader Advocate: Readability review
- Devil's Advocate: Counter-arguments and completeness
- Editor-in-Chief: Final polish and quality assurance

#### Anti-AI Pattern System

- Standalone validation skill for reusability
- Post-tool hook for automatic validation
- 3-tier detection: Forbidden, Warning, Structural
- Auto-correction suggestions for AI-like expressions

#### 8 Preset Personas

1. Architect (formal + architecture + analytical + authoritative)
2. Developer (conversational + implementation + experiential + empathetic)
3. Storyteller (narrative + experiential + experiential + empathetic)
4. Mentor (conversational + education + nurturing)
5. Analyst (technical + industry + analytical + authoritative)
6. Reviewer (technical + implementation + analytical + empathetic)
7. Curator (technical + industry + analytical + authoritative)
8. Columnist (narrative + critical + provocative)

#### Research System

- Deep web search protocol
- Media collection (images, YouTube)
- Source verification and citation system

### Changed

- Plugin name: astory-ai-authors -> astory-blog-writers
- Complete architecture redesign from fixed personas to DNA-based system
- Enhanced README with comprehensive documentation

### Technical

- Standalone plugin (no MoAI-ADK dependencies)
- No Context7 MCP references
- Standard Claude Code tools only
- Progressive disclosure skill structure

## [1.0.0] - 2026-01-05

### Added

- Initial release with 8 fixed personas
- Basic research agent
- Single writing mode
- Anti-AI pattern detection (embedded in writing-standards)

---

## Migration Guide (1.x -> 2.0)

### Breaking Changes

- Plugin name changed: Update your references from `astory-ai-authors` to `astory-blog-writers`
- Command structure changed: `/post` now includes mode selection phase

### New Features to Explore

1. Try Crew Mode for important posts: Select "Crew Mode" when prompted
2. Use Custom DNA: Select "Custom DNA" to create your own persona
3. Enable Adaptive Mode: Let the system switch personas per section

### Upgrade Steps

1. Uninstall old plugin: `/plugin uninstall astory-ai-authors`
2. Install new plugin: `/plugin install modu-ai/cc-plugins/astory-blog-writers`
3. Run `/post` to experience the new workflow
