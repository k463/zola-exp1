# maskfile

Tasks for zola-exp1. Can be run with
[mask](https://github.com/jacobdeichert/mask), or manually ofc.

## update-theme

> Update vendored theme sources.

``` sh
if ! git diff --quiet || ! git diff --quiet --cached; then
  echo "Working tree dirty, please commit or stash changes first." >&2
  git status -sb --untracked-files=no >&2
  exit 1
fi

theme_dir="themes/zola-grayscale"
vendir sync
rm -rf "${theme_dir}/.git"

if [[ -z $(git status --porcelain "${theme_dir}/") ]]; then
  echo "No changes" >&2
  exit 0
fi

git add "${theme_dir}/"
git commit \
  -m "chore(${theme_dir}): update from upstream sources" \
  -m "Update site theme from upstream sources."
```
