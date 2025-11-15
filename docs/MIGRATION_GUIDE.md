# Migration Guide for Pending Features

This guide summarizes the changes proposed in all open pull requests and highlights any configuration steps required to adopt them.

## PR #53 — 【Feat】Automate Docker Image Builds with GitHub Actions
- Summary of changes:
  - Adds a new GitHub Actions workflow (e.g., `.github/workflows/docker-build.yml`) to build Docker images automatically on branch updates.
  - Leverages standard Docker build action templates and best practices.
  - Ensures a fresh image is built on every push to the branch, improving CI coverage of containerization.
- New configuration / environment variables:
  - Optional: `REGISTRY`, `IMAGE_NAME`, `IMAGE_TAG` or similar variables if the workflow supports publishing. Check the workflow YAML for secrets such as `GHCR_PAT` or `DOCKERHUB_TOKEN`.
- Installation / usage instructions:
  - No local installation required. Once merged, push events to branches will trigger the workflow automatically.
  - To test locally, run `docker build -t <image> .` and ensure the Dockerfile builds successfully.

## PR #52 — feat: add shell completions (bash, zsh, fish)
- Summary of changes:
  - Adds static completion scripts under `shell-completions/`:
    - `claude-completions.bash`
    - `claude-completions.zsh`
    - `claude-completions.fish`
  - Provides manual installation steps since upstream integrated completion generation isn’t supported.
- New configuration / environment variables:
  - None required; users may add sourcing lines to their shell rc files.
- Installation / usage instructions:
  - Bash: `echo 'source /path/to/shell-completions/claude-completions.bash' >> ~/.bashrc && source ~/.bashrc`
  - Zsh: `echo 'source /path/to/shell-completions/claude-completions.zsh' >> ~/.zshrc && source ~/.zshrc`
  - Fish: `cp shell-completions/claude-completions.fish ~/.config/fish/completions/claude-completions.fish`

## PR #51 — Enhance Statsig event logging in GitHub workflows
- Summary of changes:
  - Extends GitHub workflow logging to include additional Statsig events for issue operations (e.g., closed as duplicates, duplicate comments).
  - Maintains consistency with existing logging patterns.
- New configuration / environment variables:
  - May require `STATSIG_SERVER_SECRET` or similar secret in repository settings if not already configured.
- Installation / usage instructions:
  - None locally. After merge, workflow runs will log the additional events automatically.
