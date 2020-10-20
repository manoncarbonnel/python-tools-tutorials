<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Env files](#env-files)
  - [Getting Started](#getting-started)
  - [Env configuration example](#env-configuration-example)
  - [Env dev configuration example](#env-dev-configuration-example)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Env files

**Table of Contents**

- [Getting Started](#getting-started)
- [Env configuration example](#env-dev-configuration-example)
- [Env dev configuration example](#env-dev-configuration-example)

## Getting Started

In all environments, the following files are loaded if they exist, the later taking precedence over the former:

- * .env                contains default values for the environment variables needed by the app
- * .env.local          uncommitted file with local overrides
- * .env.$APP_ENV       committed environment-specific defaults
- * .env.$APP_ENV.local uncommitted environment-specific overrides

Real environment variables win over *.env* files.

**DO NOT DEFINE PRODUCTION SECRETS IN THIS FILE NOR IN ANY OTHER COMMITTED FILES.**

## Env configuration example

``` .env

```

## Env dev configuration example

``` .env

```
