# aicut-render

Public repo = **unlimited free GitHub Actions minutes**. Render jobs run here on 4-core runners
(faster than the 2-CPU VPS), pulling source footage from Google Drive at runtime and pushing the
finished video back. **No footage is ever committed** — only the render scripts live here.

## How it works
1. `workflow_dispatch` triggers a render job.
2. The runner installs ffmpeg + rclone, restores the Drive config from the encrypted secret `RCLONE_CONF`.
3. It pulls the source from Drive, renders, and pushes the result back to Drive.

## Security
- The Drive credential lives ONLY as a GitHub **encrypted secret**, never in the code.
- Public-repo secrets are NOT exposed to fork PRs; only collaborators can dispatch a run.
- Logs never print the secret (passed via env, not echoed).
- TODO (recommended): replace the full-account OAuth token with a **scoped Google service account**
  shared to just the AICut Drive folders — minimum-permission instead of full Drive access.
