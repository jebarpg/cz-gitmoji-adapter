# cz-gitmoji-adapter

> Commitizen adapter formatting commit messages using gitmojis.

**cz-gitmoji-adapter** allows you to easily use gitmojis in your commits using [commitizen].

```sh
? Select the type of change you are committing: (Use arrow keys)
❯ feature   🌟  A new feature
  fix       🐞  A bug fix
  docs      📚  Documentation change
  refactor  🎨  A code refactoring change
  chore     🔩  A chore change
```

## Install

**Globally**

```bash
npm install --global cz-gitmoji-adapter

# set as default adapter for your projects
echo '{ "path": "cz-gitmoji-adapter" }' > ~/.czrc
```

**Locally**

```bash
npm install --save-dev cz-gitmoji-adapter
```

Add this to your `package.json`:

```json
"config": {
  "commitizen": {
    "path": "cz-gitmoji-adapter"
  }
}
```

ℹ️ _`pnpm` requires you to specify `node_modules/cz-gitmoji-adapter`._

## Usage

```sh
$ git cz
```

## Customization

By default `cz-gitmoji-adapter` comes ready to run out of the box. Uses may vary, so there are a few configuration options to allow fine tuning for project needs.

### How to

Configuring `cz-gitmoji-adapter` can be handled in the users home directory (`~/.czrc`) for changes to impact all projects or on a per project basis (`package.json`). Simply add the config property as shown below to the existing object in either of the locations with your settings for override.

```json
{
  "config": {
    "cz-gitmoji-adapter": {}
  }
}
```

### Configuration Options

#### Types

By default `cz-gitmoji-adapter` comes preconfigured with the [Gitmoji](https://gitmoji.carloscuesta.me/) types.

An [Inquirer.js] choices array:

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "types": [
        {
          "emoji": "🌟",
          "code": ":star2:",
          "description": "A new feature",
          "name": "feature"
        }
      ]
    }
  }
}
```

#### Scopes

An [Inquirer.js] choices array:

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "scopes": ["home", "accounts", "ci"]
    }
  }
}
```

#### Symbol

A boolean value that allows for an using a unicode value rather than the default of [Gitmoji](https://gitmoji.carloscuesta.me/) markup in a commit message. The default for symbol is false.

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "symbol": true
    }
  }
}
```

#### Skip Questions

An array of questions you want to skip:

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "skipQuestions": ["scope", "issues"]
    }
  }
}
```

You can skip the following questions: `scope`, `body`, `issues`, and `breaking`. The `type` and `subject` questions are mandatory.

#### Customize Questions

An object that contains overrides of the original questions:

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "questions": {
        "body": "This will be displayed instead of original text"
      }
    }
  }
}
```

#### Customize the subject max length

The maximum length you want your subject has

```json
{
  "config": {
    "cz-gitmoji-adapter": {
      "subjectMaxLength": 200
    }
  }
}
```


## Commitlint

Commitlint can be set to work with this package with the following configuration:

_commitlint.config.ts_

```js
import {
    RuleConfigCondition,
    RuleConfigSeverity,
    TargetCaseType,
} from '@commitlint/types';

export default {
    extends: ['gitmoji'],
    parserPreset: 'gitmoji-parser-opts',
    rules: {
        'body-leading-blank': [RuleConfigSeverity.Warning, 'always'] as const,
        'body-max-line-length': [RuleConfigSeverity.Error, 'always', 100] as const,
        'footer-leading-blank': [RuleConfigSeverity.Warning, 'always'] as const,
        'footer-max-line-length': [
            RuleConfigSeverity.Error,
            'always',
            100,
        ] as const,
        'header-max-length': [RuleConfigSeverity.Error, 'always', 100] as const,
        'header-trim': [RuleConfigSeverity.Error, 'always'] as const,
        'subject-case': [
            RuleConfigSeverity.Error,
            'never',
            ['sentence-case', 'start-case', 'pascal-case', 'upper-case'],
        ] as [RuleConfigSeverity, RuleConfigCondition, TargetCaseType[]],
        'subject-empty': [RuleConfigSeverity.Error, 'never'] as const,
        'subject-full-stop': [RuleConfigSeverity.Error, 'never', '.'] as const,
        'type-case': [RuleConfigSeverity.Error, 'always', 'lower-case'] as const,
        'type-empty': [RuleConfigSeverity.Error, 'never'] as const,
        'type-enum': [
            RuleConfigSeverity.Error,
            'always',
            [
                'style',
                'perf',
                'prune',
                'fix',
                'quickfix',
                'feature',
                'docs',
                'deploy',
                'ui',
                'init',
                'test',
                'security',
                'osx',
                'linux',
                'windows',
                'android',
                'ios',
                'release',
                'lint',
                'wip',
                'fix-ci',
                'downgrade',
                'upgrade',
                'pushpin',
                'ci',
                'analytics',
                'refactoring',
                'docker',
                'dep-add',
                'dep-rm',
                'config',
                'i18n',
                'typo',
                'poo',
                'revert',
                'merge',
                'dep-up',
                'compat',
                'mv',
                'license',
                'breaking',
                'assets',
                'review',
                'access',
                'docs-code',
                'beer',
                'texts',
                'db',
                'log-add',
                'log-rm',
                'contrib-add',
                'ux',
                'arch',
                'iphone',
                'clown-face',
                'egg',
                'see-no-evil',
                'camera-flash',
                'experiment',
                'seo',
                'k8s',
                'types',
                'seed',
                'flags',
                'animation',
                'wastebasket',
                'passport-control',
                'adhesive-bandage',
                'monocle-face',
                'coffin',
                'test-tube',
                'necktie',
                'stethoscope',
                'bricks',
                'technologist'
            ],
        ] as [RuleConfigSeverity, RuleConfigCondition, string[]],
    }
};
```
