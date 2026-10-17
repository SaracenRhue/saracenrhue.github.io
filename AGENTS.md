# AGENTS.md — saracenrhue.github.io

Personal blog built with the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)
Jekyll theme via the [chirpy-starter](https://github.com/cotes2020/chirpy-starter)
(gem) method. The theme itself is a RubyGems dependency (`Gemfile`), not a fork:
do not edit theme internals here; customize through `_config.yml`, `_data/`, and content.

## Deployment

Pushing to `main` triggers `.github/workflows/pages-deploy.yml`, which builds and
deploys the public site at https://saracenrhue.github.io. Treat pushes as
production deployments and confirm with the user first unless they have
explicitly authorized the push. Commits should use descriptive messages
(e.g. `chore: upgrade to 7.6.0`), not single letters.

## Updating the theme

Follow the official Upgrade Guide (wiki → Upgrade-Guide) via the squash-merge
procedure, or the `chirpy-update` skill if it is installed. Summary:

```bash
git fetch chirpy --tags                          # remote "chirpy" → cotes2020/chirpy-starter
git merge vX.Y.Z --squash --allow-unrelated-histories
# resolve per the ownership table below, then:
bundle update
JEKYLL_ENV=production bundle exec jekyll build   # must pass before committing
```

This repo shares no git history with the starter (normal for starter-generated
repos); `--allow-unrelated-histories` is required. Last update: 2026-10-17, to
`jekyll-theme-chirpy` 7.6.0.

## File ownership

Starter-owned — take the starter's side on updates:

- `README.md` (stock starter text; an earlier update left conflict markers
  committed in it — keep it stock from now on), `Gemfile`, `LICENSE`,
  `index.html`, `.github/`, `.devcontainer/`, `.vscode/`, `.editorconfig`,
  `.gitattributes`, `.gitignore`, `.gitmodules`, `.nojekyll`, `_plugins/`,
  `_data/share.yml`, `_tabs/archives.md`, `_tabs/categories.md`,
  `_tabs/tags.md`, `tools/`, `assets/lib` (gitlink submodule).

User-owned — never overwrite:

- `_posts/**` (all posts), `_tabs/about.md` (personal bio), `_data/contact.yml`
  (includes a Stack Overflow link), `logo.png` (avatar), `assets/img/favicons/`
  (every file is the user's logo; the theme gem's defaults are overridden by them).

Delete on update if present (stale, now provided by the theme gem where local
copies would override the gem's current versions):

- `_data/locales/`, `_data/assets/`, `tools/deploy.sh` (replaced by `tools/run.sh`).

## Personal `_config.yml` values

When merging a new starter `_config.yml`, re-apply these site values:

- `timezone: Europe/Vienna`, `lang: en`
- `title: Saracen Rhue`, `tagline: coding dictionary`
- `description`: "A blog containing various articles about programming, linux and macOS."
- `url: "https://saracenrhue.github.io"`, `baseurl: ""`
- `github.username: saracenrhue`, `twitter.username: SaracenRhue`
- `social`: name Saracen Rhue, email mail@saracenrhue.ch, links → Twitter, GitHub
- `theme_mode: dark`, `avatar: './logo.png'`, `toc: true`, `paginate: 10`
- `pwa.enabled: true` (plus the starter's `pwa.cache` defaults)
- Comments, analytics, and verification keys stay empty.

## Build and test

```bash
bundle install                                  # after Gemfile changes
JEKYLL_ENV=production bundle exec jekyll build  # production build
bundle exec jekyll serve                        # local preview at :4000
tools/test.sh                                   # html-proofer (optional)
```

Local toolchain: system Ruby + Bundler (verify with `ruby -v`, `bundle -v`).
