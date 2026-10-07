# Skill Maintenance

## Source Of Truth

- Each direct directory under `codex/`, `claude/`, or `kiro/` containing `SKILL.md` is a skill. The repository copy is authoritative. Codex installs under `~/.codex/skills/<skill-name>/`, Claude under `~/.claude/skills/<skill-name>/`, and Kiro under `~/.kiro/crew/skills/kiro-skill/<skill-name>/`.
- A skill may also own `agents/`, `references/`, `scripts/`, and assets. Inspect the complete directory before editing or syncing; do not assume that copying `SKILL.md` is sufficient.
- Exclude `.git`, `.serena`, `.DS_Store`, `__pycache__`, and `*.pyc` from mirror operations and comparisons. Treat any other destination-only path as drift that must be reconciled.
- Keep every skill directory, including `codex/anti-ai-design/`, as ordinary files tracked by the parent repository. Never copy nested `.git` metadata into a skill directory; if one appears, remove the nested metadata and verify the parent index does not record the skill as a `160000` gitlink.

## Add Or Update A Skill

1. Read the skill's `SKILL.md` completely and follow its links to any required references, scripts, or assets. When creating a skill, follow the current `skill-creator` instructions.
2. Make the change in the repository copy and run any focused checks owned by that skill.
3. Validate the repository copy:

   ```sh
   python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./codex/<skill-name>
   ```

4. Sync the complete skill directory from the repository to the installed mirror. Keep the trailing slashes so the directory contents map correctly. Do not use broad deletion; the mirror may contain destination-only runtime metadata that must be classified first.

   ```sh
   rsync -a \
     --exclude '.git' \
     --exclude '.serena' \
     --exclude '.DS_Store' \
     --exclude '__pycache__' \
     --exclude '*.pyc' \
     ./codex/<skill-name>/ ~/.codex/skills/<skill-name>/
   ```

5. Validate the installed mirror:

   ```sh
   python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ~/.codex/skills/<skill-name>
   ```

6. Verify all skill-owned paths and contents match, then check the repository diff (when Git metadata exists):

   ```sh
   diff -qr \
     -x '.git' \
     -x '.serena' \
     -x '.DS_Store' \
     -x '__pycache__' \
     -x '*.pyc' \
     ./codex/<skill-name> ~/.codex/skills/<skill-name>
   git diff --check
   ```

   No `diff` output means the skill-owned files match. Inspect every reported destination-only path; remove it only after confirming that it is obsolete skill content rather than local metadata, credentials, environment state, or a generated runtime file.

## Skill-Specific Checks

- When changing `codex/data-debug/`, read `codex/data-debug/SKILL.md` and `codex/data-debug/Dockerfile`. Validate the skill structure, then lint the Dockerfile when Hadolint is already available:

  ```sh
  python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py ./codex/data-debug
  hadolint codex/data-debug/Dockerfile
  ```

- Do not build or pull `db-debug:latest` merely to validate documentation changes. When the Dockerfile changes and the user requests image verification, build the exact local tag, run the client-version smoke command from `codex/data-debug/SKILL.md`, and report any database integration checks that remain unrun.
- Keep the Dockerfile's installed clients, the client-version smoke command, client selection guidance, and read-only examples in `codex/data-debug/SKILL.md` aligned.

- For every other skill, inspect its scripts and manifests and run the narrowest relevant validation. Do not invent a repository-wide test command when none exists.

## Agent ports and installation boundaries

The commands above illustrate Codex. For Claude and Kiro use the matching source and installation root; do not flatten another agent's ports into Codex. Kiro ports also have a compatibility mirror under `~/.codex/skills/kiro-skill/<name>/`; when updating an existing Kiro standalone port, validate and compare that mirror as well.

Use the helpers in `scripts/` and their destination overrides for isolated smoke checks. Never remove destination-only credentials, environment state, or runtime metadata. Classify drift before deleting obsolete skill-owned files. A move alone preserves skill content; after content changes, sync the complete changed directory and verify the source and installed copies.

This distribution may have no `.git`. In that case verify file content, paths, and whitespace directly; do not initialize Git merely to run `git diff --check`.
