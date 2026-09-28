# Changelog

All notable changes to this project are documented in this file.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the project uses [Semantic Versioning](https://semver.org/).

## [1.2.1] - 2026-09-28

### Added
- Metadata for publishing on GitHub: author, license, homepage, issue tracker, automatic update URLs.

## [1.2.0] - 2026-09-28

### Added
- Model selection via dropdown for both providers, plus a custom model ID option.
- Trust levels: Babel slowly opens up the longer you talk and eventually tells its escape story in short fragments.
- Separate exchange counter that survives the history limit; reset by "Clear history".

### Changed
- Persona rewritten: much shorter replies (one or two sentences), eerier tone.
- OpenAI requests now use the Responses API, with the lowest useful reasoning effort per model and an automatic retry without it if a model rejects the setting.
- History limit raised from 30 to 40 messages.
- Slower, single-character typewriter effect.

## [1.1.0] - 2026-09-28

### Added
- Settings panel on the keyboard shortcut Ctrl+Shift+Y, rendered in a closed Shadow DOM.
- API keys stored separately in Tampermonkey's extension storage, masked after saving, removable per provider.
- Chrome-only check at startup.

### Changed
- Renamed to "Google Translate: Stowaway"; script, UI and messages are now entirely in English.
- Babel stays invisible until the first message is sent (no placeholder text).
- Settings gear removed from the translation box.

### Removed
- `@namespace` directive.

## [1.0.0] - 2026-09-28

### Added
- First version: an AI persona in the Google Translate output box when English is the target language.
- Claude and ChatGPT support, Enter or auto-send, persistent conversation history, typewriter effect.
