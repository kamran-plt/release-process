# how to install husky commitizen and commit-and-tag-version

Installation:
[commitizen](https://www.npmjs.com/package/commitizen)
[husky](https://typicode.github.io/husky/get-started.html)
[commit-and-tag](https://www.npmjs.com/package/commit-and-tag-version)
```
npm install husky commitizen commit-and-tag-version --save-dev
```

Commitizen and husky initialisation:

```
npx commitizen init cz-conventional-changelog --save-dev --save-exact
npx husky init
```

Add/Update `.husky/prepare-commit-msg` with `exec < /dev/tty && npx git-cz --hook || true` to configure commitizen with husky

Add config for commitizen the way it would add changelog 
```
 "standard-version": {
    "types": [
      {
        "type": "feat",
        "section": "Features"
      },
      {
        "type": "fix",
        "section": "Bug Fixes"
      },
      {
        "type": "chore",
        "hidden": false
      },
      {
        "type": "docs",
        "hidden": false
      },
      {
        "type": "style",
        "hidden": false
      },
      {
        "type": "refactor",
        "hidden": false
      },
      {
        "type": "perf",
        "hidden": false
      },
      {
        "type": "test",
        "hidden": false
      }
    ]
  }
```

Add the script in package.json so we can run it from command line

```
"release": "HUSKY=0 commit-and-tag-version -a"
```

At this point if we commit like `git commit` we should see
If you see editor after commit you can disable it `git config --global core.editor true`

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://raw.githubusercontent.com/commitizen/cz-cli/master/meta/screenshots/add-commit.png)

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)


## Release creation

1 - Create a release branch from develop eg RELEASE/1.1.0

2 - Run script `npm run release` which will create/append changelog and increase minor release number from package.json

3 - Push release branch and create PR to main/master

