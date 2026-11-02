# Maintaining parth-community

This repository is documentation and an issue tracker only. The source code is in a private repository.

## One-time GitHub setup

Do these once, in this repository's **Settings**:

1. **General → Features:** turn on **Issues** and **Discussions**. The issue forms link to Discussions for questions.
2. **Pages:** Source **Deploy from a branch**, branch `main`, folder `/docs`. The site is then at <https://rslakra.github.io/parth-community/>. Check **Enforce HTTPS**.
3. **Code security:** turn on **Private vulnerability reporting**. [SECURITY.md](SECURITY.md) and the issue chooser point at it.
4. **Discussions:** keep the default categories. Q&A is where questions go.
5. **Labels** (Issues → Labels): `bug`, `enhancement` and `documentation` exist by default, and the forms apply them. Optional, for triage: `ide: vscode`, `ide: cursor`, `ide: jetbrains`, `needs-info`, `duplicate`. The forms ask which IDE it is, so you can label by hand in seconds.
6. **Branch protection** on `main` (optional): require a pull request, so the live site only changes after review.

## Preview the site on your computer

```bash
cd docs
bundle install
bundle exec jekyll serve --baseurl /parth-community
# open http://127.0.0.1:4000/parth-community/
```

Pages are plain Markdown with a small front matter block (`title`, `parent`, `nav_order`). The theme is [just-the-docs](https://just-the-docs.com/).

- Link to another page with a normal relative link: `[Connect a provider](connect-provider.md)`.
- Add a screenshot with the include: `{% include screenshot.html src="composer.png" width="320" alt="..." %}`. Put the file in `docs/assets/screenshots/`.
- A callout is a paragraph that follows `{: .note }`, `{: .tip }` or `{: .warning }`.

## On every release of Parth

1. Add the new version's notes to `docs/changelog.md` (copy them from the product's CHANGELOG).
2. Check these pages against what changed, and fix them: [install pages](docs/install/), [settings](docs/setup/settings.md), and any screenshot that no longer matches the UI.
3. If a known issue was fixed or a new one appeared, edit `docs/troubleshooting.md`.
4. If the marketplace listings or links changed (Open VSX, JetBrains Marketplace), edit `README.md` and `docs/install/`.

The docs are ported from the product's README, `docs/CUSTOM_PROVIDERS.md`, `docs/LOCAL_MODELS.md`, `PRIVACY.md` and `SECURITY.md`. When one of those changes in the source repository, make the same change here.

## Screenshots still to take

The install pages mark where a screenshot would help with an HTML comment (`<!-- screenshot needed: … -->`). Search for it:

```bash
grep -rn "screenshot needed" docs
```

Save each one in `docs/assets/screenshots/` with the name in the comment, then replace the comment with the `screenshot.html` include.

## Triage

- A bug without an IDE, version or log: label `needs-info` and ask for them (link [How to report a problem](https://rslakra.github.io/parth-community/report-an-issue/)).
- Copy the confirmed bug or accepted feature into the private tracker, and link it back in a comment.
- Security reports must move to a private advisory right away. Delete anything sensitive that someone posted publicly.
