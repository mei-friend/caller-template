# mei-friend automation setup - caller template

This is a **GitHub repository template** for setting up a caller repository that works with [mei-friend](https://mei-friend.github.io)'s GitHub Actions automation.

To use it, click **"Use this template"** on GitHub to create your own repository — do not fork and edit this template directly. Then add your MEI files and trigger work packages from mei-friend.

For the full documentation, see [Automation in mei-friend](https://mei-friend.github.io/docs/advanced/automation/).

---

## Role in the automation architecture

A caller repository is the user's own GitHub repository where MEI files are stored and versioned. It contains a single small workflow file (`.github/workflows/caller.yml`) that:

1. Receives a `workflow_dispatch` event from mei-friend (sent via the GitHub API when the user triggers a work package).
2. Checks out both this caller repository and the specified **central repository** (at the specified branch).
3. Runs the automation script from the central repository against the MEI file in this repository.
4. Commits any results back to this caller repository.

The central repository, branch, and script path are passed as inputs with each dispatch — meaning different work packages can point to different central repositories or branches without any changes to `caller.yml`.

---

## Quick start

1. Click **"Use this template"** on this repository's GitHub page to create your own caller repository.
2. Add your MEI files to it (or keep the demo files for testing).
3. In mei-friend, open **Settings > mei-friend > Use GitHub Actions** and check **"Show available GitHub Actions"**.
4. Paste the URL of a JSON work package definition into the **"Custom configuration"** field. For testing, use:
   `https://raw.githubusercontent.com/mei-friend/automation/refs/heads/main/work_packages.json`
5. Log in to GitHub in mei-friend and open a file from your caller repository.
6. From the GitHub menu, click **"GitHub Actions: Call automation workflow"**, choose a work package, fill in any parameters, and click **"Run workflow"**.

You need write access to the caller repository so that processing results can be committed back.

---

## Switching central repository

Each work package definition in the JSON configuration specifies which central repository to use via three fields:

```json
{
  "central_repository": "mei-friend/automation",
  "branch": "main",
  "automation": "automation/run_automation.sh",
  "work_packages": [...]
}
```

- **`central_repository`** — the `owner/repo` of the repository containing the automation logic.
- **`branch`** — the branch of that repository to check out.
- **`automation`** — the path to the entry-point script within that repository.

mei-friend reads these fields from the work package and passes them as inputs when dispatching `caller.yml`. To point to a different central repository (e.g. a project-specific one), update these fields in the work package JSON — no changes to `caller.yml` are needed.

See [Setting up your own central repository](https://mei-friend.github.io/docs/advanced/automation/#setting-up-your-own-central-repository) for the full setup.

---

## Demo encodings included in the template

The template ships with two MEI files for testing the automation flow without having to upload your own data:

- **"Mondnacht am Meer"** for voice and piano by Ludwig Baumann, held in Badische Landesbibliothek Karlsruhe. _3 Lieder — Mus. Hs. 1324: V, pf / Ludwig Baumann._ [S.l.], 18XX. Badische Landesbibliothek Karlsruhe, Mus. Hs. 1324. <https://nbn-resolving.org/urn:nbn:de:bsz:31-57896> — License: CC BY-SA 4.0. Encoding by [@annplaksin](https://github.com/annplaksin).
- **6 Variations on "Nel cor più non mi sento"** (WoO 70) by Ludwig van Beethoven, Breitkopf und Härtel edition, 1862–90, plate B.168. License: CC BY 4.0. Encoding by [@wergo](https://github.com/wergo).
