# testing-rep

This repository includes Git hook support for AI-generated code tracking.

- `.github/copilot-instructions.md` defines AI tagging conventions.
- `.git/hooks/pre-commit` counts AI-generated lines and strips tag markers before commit.
- `.git/hooks/commit-msg` appends `AI-Lines-Of-Code: <count>` to the commit message when AI-generated lines are present.
