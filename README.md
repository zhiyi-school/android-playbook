# android-playbook

Android mobile application security playbooks documenting platform features, the risks associated with those features, and application controls that address those risks.

Playbook documents live under `playbooks/`. Each feature can have multiple risk entries, and each risk can have multiple control entries.

## Repository structure

```text
playbooks/
├── android-platform-feature-*.md
├── sample-apps/          # Sample application source projects
├── assets/              # Screenshots and supporting media
├── control-examples/    # Projects or APKs demonstrating security controls
└── demo-scripts/        # Scripts used in playbook demonstrations
docs/                   # Repository and authoring documentation
examples/               # Example playbook submissions and templates
scripts/                # Repository validation and review tooling
.github/workflows/      # GitHub Actions review workflows
```

`playbooks/assets/` contains screenshots extracted from the Android mobile app security guide. The other supporting folders are currently empty. Root-level `scripts/` is reserved for repository tooling; `playbooks/demo-scripts/` is reserved for demonstration scripts.

## Playbook coverage

The repository currently contains 7 feature entries, 11 risk entries, and 13 control entries covering:

- APK acquisition
- USB debugging
- HTTP proxy configuration
- Overlays
- Accessibility services
- Screen recording
- Rooting

## Expected filename patterns

- Feature: `android-platform-feature-01.md`
- Risk: `android-platform-feature-01-risk-01.md`
- Control: `android-platform-feature-01-risk-01-control-01.md`

Use two-digit identifiers, such as `01`, `02`, and `03`, for each feature, risk, and control. Keep the document's top heading consistent with its filename.

## Document format

Each entry includes a top-level identifier, a `Title`, a `Description`, and a `Demonstration` with descriptive numbered step headings such as `#### 01. Prepare the environment`.

Feature entries also include `Additional context` and links to related risks. Risk entries include a `Goal`. Some control descriptions still contain `Insert here` placeholders.

Use relative paths from the playbook document when linking supporting files, for example `assets/example.png` or `control-examples/example.apk`.

## Review status

Review is currently manual. No automated validator, advisory AI reviewer, or GitHub Actions review workflow is configured in this repository.

The following review phases are proposed, following the iOS playbook repository's approach:

1. **Format validation:** filename and heading consistency, required sections, internal links, Markdown tables, trailing whitespace, and unreplaced placeholders.
2. **Advisory clarity review:** ambiguous wording, section flow, demonstration steps, and terminology consistency.
3. **Advisory technical completeness review:** Android-specific accuracy, unsupported claims, missing assumptions, and gaps in demonstration sequences.

Local review commands and CI instructions should be documented here when the corresponding tools are implemented.

## Manual review checklist

1. Check filenames, headings, and related-entry links against the Android naming convention.
2. Confirm that required sections and demonstration steps are complete, including any remaining placeholders.
3. Verify that local links and image paths resolve to files in the repository.
4. Check technical content against the approved Android mobile app security guide, which is the source of truth.
5. Confirm that formatting changes preserve the original wording and commands; review content corrections separately.
