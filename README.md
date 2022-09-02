# GitHub Packages

This document is for the purpose of helping and instructing developers on how to
setup their local environments so that they may download private packages from GitHub.

## Obtain Personal Token

First step is to obtain a personal access token from GitHub. In order to do so perform
the following:

1. Log into GitHub
2. In the top right corner click your profile photo and select **Settings**
<img width="250" alt="image" src="https://user-images.githubusercontent.com/5088893/188146247-0b0ac2e6-65f9-4fca-8119-b86aa5e86996.png">


3. From the side panel select **Developer settings > Personal access tokens** near the bottom.
4. Click **Generate new token**
Note: **GitHub Packages ReadOnly**
Expiration: **30 days**
<img width="686" alt="image" src="https://user-images.githubusercontent.com/5088893/188147183-4230238d-4108-45e4-832c-10c74cf41f42.png">

5. Click save and copy your new token

## Store Personal Token

You can insert your new token into you shell with the following:

    $ export GITHUB_PKG_REG_TOKEN=<paste your token>

If you'd like for this variable to be available always you can copy that line to your
bash profile (`.zshenv` for Mac OS).

The naming `GITHUB_PKG_REG_TOKEN` is important as this variable is injected into docker when installing
new packages.

## Docker Setup

N/A

## Local Setup

In order to be setup locally we need to tell bundler and npm how to authenticate with our
GitHub registry.

### NPM

In the project directory run:

    $ echo "//npm.pkg.github.com/:_authToken=$GITHUB_PKG_REG_TOKEN" > .npmrc

> The `.gitignore` file should already contain the `.npmrc` file but just in case
> do not add it to version control.

### Bundler

Add this line to your shell or bash profile (`.zshenv` for Mac OS)

    $ export BUNDLE_RUBYGEMS__PKG__GITHUB__COM=$GITHUB_PKG_REG_TOKEN

This is equivalent to using bundle config

    $ bundle config rubygems.pkg.github.com $GITHUB_PKG_REG_TOKEN
