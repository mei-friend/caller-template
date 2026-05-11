# mei-friend automation setup - caller template

This is a **GitHub repository template** for setting up a caller repository that works with [mei-friend](https://mei-friend.github.io)'s GitHub Actions automation. For the full documentation, see [Automation in mei-friend](https://mei-friend.github.io/docs/advanced/automation/).

To use the template, click **"Use this template"** on GitHub to create your own repository — do not fork and edit this template directly. Add your MEI files to your repository and trigger work packages from mei-friend's GitHub Actions panel.

---

## Role in the automation architecture of mei-friend

A caller repository is the user's own GitHub repository where MEI files are stored and versioned. It contains a single small workflow file (`.github/workflows/caller.yml`) that:

1. Receives a `workflow_dispatch` event from mei-friend (sent via the GitHub API when the user triggers a work package).
2. Checks out both this caller repository and the specified **central repository** (at the specified branch).
3. Runs the automation script from the central repository against the MEI file in this repository.
4. Commits any results back to this caller repository.

The central repository, branch, and script path are passed as inputs with each dispatch — meaning different work packages can point to different central repositories or branches without any changes to `caller.yml`.

---

## Step-by-step instructions for setting up a caller repository

1. Click **"Use this template"** on this repository's GitHub page to create your own caller repository.
2. Add your MEI files to it (or keep the demo files for testing).
3. In mei-friend, open **Settings > mei-friend > Use GitHub Actions** and check **"Show available GitHub Actions"**.
4. Paste the URL of a JSON work package definition into the **"Work package definition"** field. For testing, use:
   `https://raw.githubusercontent.com/mei-friend/automation/refs/heads/main/work_packages.json`
5. Log in to GitHub in mei-friend and open a file from your caller repository.
6. From the GitHub menu, click **"GitHub Actions: Call work package workflow"**, choose a work package from the dropdown in the GitHub Actions panel, fill in any parameters, and click **"Run workflow"**.

You need write access to the caller repository so that processing results can be committed back.

For a more detailed walkthrough, see [Step-by-Step instructons](https://mei-friend.github.io/docs/advanced/automation/#step-by-step-instructions) in the mei-friend documentation.

---

## Demo encodings included in the template

The template ships with two MEI files for testing the automation flow without having to upload your own data:

- **"Mondnacht am Meer"** for voice and piano by Ludwig Baumann, held in Badische Landesbibliothek Karlsruhe. _3 Lieder — Mus. Hs. 1324: V, pf / Ludwig Baumann._ [S.l.], 18XX. Badische Landesbibliothek Karlsruhe, Mus. Hs. 1324. <https://nbn-resolving.org/urn:nbn:de:bsz:31-57896> — License: CC BY-SA 4.0. Encoding by [@annplaksin](https://github.com/annplaksin).
- **6 Variations on "Nel cor più non mi sento"** (WoO 70) by Ludwig van Beethoven, Breitkopf und Härtel edition, 1862–90, plate B.168. License: CC BY 4.0. Encoding by [@wergo](https://github.com/wergo).
