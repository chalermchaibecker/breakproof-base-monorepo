<div align="center">

<picture><img alt="Breakproof Base Repo BETA VERSION" src="../docs/logo-big.svg" height=175px /></picture>

![Linux is supported](https://img.shields.io/badge/Linux-Supported-pass)
![macOS is supported](https://img.shields.io/badge/macOS-Supported-pass)
![Windows is not supported](https://img.shields.io/badge/Windows-Not%20Supported-red)

<a name="breakproof-nav"></a>

🎯 [The problems it solves](#the-problems-it-solves) — 💡
[How it works](#how-it-works) — 🚀
[Getting started](#getting-started-with-your-breakproof-repo) — 🏆
[List of Best Practices](#best-practices-list)

⚙️ [Tools & Configuration](#tools-list) — ⚖️
[Conventions](#conventions-and-core-principles) — 📋️ [What's next](#whats-next)

<sub>[How can tools use different node.js?](#how-separate-nodejs)</sub>

</div>

```bash
# first, <create your empty github repo>
git clone <YOUR REPO URL>
git remote add breakproof git@github.com:YotpoLtd/breakproof-base-monorepo.git
git pull breakproof main
pnpm --workspace-root generate repo init
```

# TLDR;

### What is The Breakproof base monorepo?

📄 A pnpm monorepo template **meant to be cloned** and used for your projects.

The breakproof monorepo template comes with ready to be used
[tools already in it](#tools-list), where each tool lives in
**[its own package](#how-separate-nodejs)**, runs
**[its own version of Node.js](#how-separate-nodejs)** and provides
[**strict default config**](#tools-list) to be consumed by your projects and the
**built-in optimized CI/CD**

🔀 **Clone** to create your own monorepo! — 🔄 **Pull** to update the tools &
CI/CD!

### The immediate value of developing inside breakproof monorepo

Your clone 🔀 becomes a **_breakproof home_** 🏠 where you can develop **your
frontend projects** without 💥 _**breaking your code**_ or 💰
_**breaking**-**the**-**bank**_.

You start by **importing your existing** projects or **generating new** ones. ⚡
**_Immediately_** those projects get a ton of **working** processes like
**optimized** CI/CD, **meticulous** code checks, **automatic** `npm` releases,
**precise** code-editor integration, etc. **_And because_** you cloned the repo,
you keep receiving updates for those processes simply via `git pull`.

**You get:**

1. 🚀️ _laser-focus_ on **_your projects_** — _not on the tooling around them_

2. 🔄 _easier upgrades_ of **_your projects_** — _due to full isolation between
   tools & projects (even different
   <img src="https://custom-icon-badges.demolab.com/badge/node.js-E0DDCE?logo=nodedotjs&logoColor=323330&labelColor=F0DB4F&style=flat-square" alt="node.js" valign="middle" />
   versions)_

3. 🧹 **_low-to-none_** repository **_maintenance_** — _the breakproof repo will
   update **tooling & processes** around your projects, keep them **optimized**
   & following **best practices**, without you having to change your code_

> [!NOTE]
>
> All of that 🔼 is implemented by making
> [**industry-standard tools 🏆**](#tools-list) work together, **_NOT_**
> introducing "_yet-another-abstraction_" and **_NOT_** requiring specific
> project tech stack.

<a name="the-problems-it-solves"></a>

# 🎯 What problems does your `Breakproof Base Repo` clone solve?

<picture><img alt="project-vs-tools-problem" src="/docs/project-vs-tools.svg" /></picture>

🛠️ You want to **focus building your project**, not waste time in upgrading the
tooling around it or making different tools for code checks, testing, build &
release behave well together or with your code editor, **_BUT at the same
time_** you want to get the bug fixes and performance improvements from latest
versions of all tools 🤔 ([solution in next section](#how-it-works)).

<p> </p>

<picture><img alt="project-vs-cicd-problem" src="../docs/project-vs-cicd.svg" /></picture>

👨‍🔧 It's hard to create a well-optimized, precise & cost-effective CI/CD that
doesn't break with scale and informs developers what is going to happen without
noise. You want someone else to create & maintain 90% of CD/CD processes,
without requiring your projects to have specific tech stack 🤔
([solution in next section](#how-it-works)).

<p> </p>

<picture><img alt="project-vs-upgrade-problem" src="../docs/project-vs-upgrade.svg" /></picture>

🗄 You **cannot regularly stop** development until you upgrade everything
everywhere, you want to do it **piece by piece in isolation** 🤔
([solution in next section](#how-it-works)).

<p> </p>

<picture><img alt="project-vs-strictness" src="../docs/project-vs-strictness.svg" /></picture>

🕊 You want to improve your codebase but cannot fix all problems at once. You
need to be **tolerant of existing problems** but **forbid new problematic code**
🤔 ([solution in next section](#how-it-works)).

<p> </p>

<picture><img alt="project-vs-yet-another-config-and-wrapper" src="../docs/project-vs-yet-another-config-and-wrapper.svg" /></picture>

🥴 You are **tired of learning new configuration formats** with each new
repo-management tool that comes out and then **hitting its customization
limits**. You want to **directly deal with the tools** used but still rely on
**sensible default configuration** you can extend 🤔
([solution in next section](#how-it-works)).

<p> </p>

<picture><img alt="project-vs-industry-standard-and-swap" src="../docs/project-vs-industry-standard-and-swap.svg" /></picture>

🏆 You want to use industry-standard best practices without having to design the
entire process from scratch, **_BUT at the same time_** be free to swap
individual tools without having to redo the entire system 🤔
([solution in next section](#how-it-works)).

<p> </p>

[⬆️ Back to top nav ⬆️](#breakproof-nav)

<p> </p>

<a name="how-it-works"></a>

# 💡 How does `Breakproof Base Repo` solve those problems?

<picture><img alt="Breakproof package isolation" src="../docs/breakproof-isolation.svg" /></picture>

- The repo is a `pnpm` workspace — _a.k.a._ monorepo managed only using `pnpm`
  without any abstraction on top of it. This, by itself, lets you isolate one
  project from another by making each a separate package. The breakproof repo
  goes **_a step further_**.

- <a name="how-separate-nodejs"></a> When using the breakproof repo, your
  projects are isolated from the tools they use. This is achieved by installing
  the tools in a separate package instead of the same package as your project.
  In fact each different tool is installed in its own individual package. This
  allows us to
  [leverage an ability of `pnpm` to specify a different `node.js` for each package](https://pnpm.io/package_json#devenginesruntime).
  Essentially you get an isolated pair of `<tool> + <node.js>`, e.g.
  `eslint + node22` and this lets you run `eslint`(_using `node22`_) from any
  place in the repo with a `pnpm` command similar to:
  `pnpm --filter=<PACKAGE NAME THAT INSTALLS TOOL IN IT> run <TOOL NAME>`. For
  example: `pnpm --filter="@repo/eslint-isolated-base" run eslint`

- The breakproof repo comes with several tool packages already in it, each
  installs one industry-standard tool like `eslint`, or `TypeScript`, or
  `rollup`, or `jest`, …[_( full list below ⬇️ )_](#tools-list). Additionally,
  each of those packages include **detailed & strict base configuration** for
  the specific tool that your projects can extend. This means **your projects
  are in full control** of the final tool configuration. If one package needs a
  tool, it calls a script from another package that installs that tool. That's
  it. 🔄 Each individual tool can be swapped with another as long as it does
  it's job. _([role of each tool is listed below ⬇️](#tools-list)_

- On many occasions the base configuration is tweaked so it accounts for
  limitation of another tool, thus making them behave well together. Not all
  tools accept all their settings through a config file, some require CLI
  arguments. For those occasions, each package that contains an isolated tool
  defines a command in the "script" section of its `package.json` to act as a
  shortcut. This shortcut can be executed from anywhere running:
  `pnpm --filter=<PACKAGE NAME THAT INSTALLS TOOL IN IT> run <SHORTCUT NAME>`

- The above 🔼 means that suddenly you can upgrade one tool in complete
  isolation from the rest & your project, even if the newer version requires a
  newer `node.js` version. This will not affect other packages. It also means
  your code can use whatever `node.js` version you need while some useful tool
  is "stuck" in the past without dragging you down

<p> </p>

<picture><img alt="Breakproof CI/CD setup" src="../docs/breakproof-cicd.svg" /></picture>

- The CI/CD process is implemented as GitHub actions/workflows. Because it knows
  the repo uses `pnpm`, we can target only a subset of the packages inside it
  when running tasks. For example, if a PR only changes your project, then the
  CI/CD will run test & linting checks **only for your project**. It will also
  run them in parallel and install only the dependencies that your project
  needs, which are cached, so subsequent runs with the same dependencies don't
  waste time re-downloading them.

- The only requirement from your projects to participate in the CI/CD is to
  define properties in the `"scripts"` section of their `package.json` with
  specific names (_a convention_). You can run whatever command you like there,
  but probably you will run some of the isolated tools as shown above. For
  example, if you want your project tested in GitHub PRs, the project must
  define a `lint:github-pr` script with value of
  `pnpm --filter='@repo/jest-base-isolated' run jest` where
  `@repo/jest-base-isolated` is just the name of the package that isolates
  `jest`. The convention for the names of those scripts is as straightforward as
  possible, so you need `build` for building, `release` for `npm` releases, etc.

- Because the CI/CD is a GitHub action, it easily posts comments on your PRs
  with useful info about the upcoming releases when PR is merged, or summary of
  code problems found in the changed packages. The CI/CD will also run specific
  checks for repository [conventions](#conventions-and-core-principles) like
  making sure every `package.json` explicitly defines desired `node.js` version
  to use. The breakproof repo even implements
  [GitHub job summary](https://github.blog/news-insights/product-news/supercharging-github-actions-with-job-summaries/)
  which allows for a friendly way to overview the progress of the running
  workflow without the noise of going through logs.

- You can implement your custom CI/CD bits like running deployment as just
  another GitHub workflow, **_BUT_** with the benefit that your workflow can
  receive extra inputs — the list of packages that have been changed or the list
  of packages that will be automatically released to `npm`. You can then use
  that information to only trigger logic in certain cases.

<picture><img alt="Tolerance for past problems" src="../docs/breakproof-snapshot-errors.svg" /></picture>

- To allow you to work on projects that have some code problems **_BUT at the
  same time_** stop new problems from popping up, the breakproof repo has
  created a few `node.js` scripts inspired by `esplint` that basically
  "snapshots"/"remembers" what kind of problems each of your files have and how
  many occurrences per problem type there are. This allows you to ignore the
  existing ones but error out if the number of problems increase. This same
  ability of "remembering existing problems" is useful when tools are upgraded
  or their configuration changes. At this point they can become stricter or
  change the way they detect problems. To unblock the upgrade without investing
  immediately investing time you can snapshot the new results and continue with
  your day.

<p> </p>

[⬆️ Back to top nav ⬆️](#breakproof-nav)

<p> </p>

<a name="getting-started-with-your-breakproof-repo"></a>

# 🚀 Get started with _your_ `breakproof` repo

1. 🔀 **Clone this repo.** (_and then push it to your own blank repo_)

2. 🎛️ Initialize your clone with your preferences & automatically configure your
   code editor:

   ```shell
   pnpm --workspace-root generate repo init
   ```

3. 🚀 [Generate new](../docs/pnpm-intro.md#creating-a-new-package-in-the-repo)
   or
   [import your existing](./infra/devx-and-repo/repo-shell-scripts/README.md#using-import-from-other-repo)
   projects.

<a name="automatic-npm-publishing"></a>

### If you want to automatically release projects as `npm` packages

<details>
<summary>Expand to see steps for setting up automatic publishing</summary>

You need to add some GitHub configuration for your repository:

1. Create a
   [`bot`/ `machine` GitHub account](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service#3-account-requirements)
   that will be used **_ONLY_** for the automatic release process. Using email
   like `bot@<your domain>.com`.

2. Set up GitHub repository `variable`s:

- `AUTORELEASE_BOT_NAME` – the name to be used as commit author of the automatic
  version changes to your main branch
- `AUTORELEASE_BOT_EMAIL` – the email associated bot account you've created; to
  be used as commit author of the automatic version changes to your main branch

3. Set up GitHub repository `secret`s:

- `AUTORELEASE_BOT_TOKEN`: a
  [GitHub token with rights to push to repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#personal-access-tokens-classic)
  to be used by the bot doing automatic releases
- `NPM_REGISTRY_USER`: your npm registry user
- _\[Optional\]_ `NPM_REGISTRY_AUTH_TOKEN`: your npm registry auth token, if you
  don't use a password instead
- _\[Optional\]_ `NPM_REGISTRY_PASSWORD`: your npm registry password if you use
  this instead of auth token

4. Set up GitHub Merge Queue:

- Head to
  `<your github repo> -> Settings -> Rules -> Rulesets -> New ruleset -> Import a ruleset`
- And upload `<repo root>/.github/branch-rulesets/Default Branch.json`. This
  will:

  - Require a `Merge Queue` for your default branch.
  - Require `basics` job from the main GitHub workflow to pass before PRs can be
    merged

  The above is used to make sure that no PR is merged while the CI for automatic
  releases of `npm` packages is running. This CI job can push version bumps &
  changelogs to your default branch. Without the merge queue there is a risk of
  a race condition.

5. Write the steps in `<repo root>/.github/actions/npm-login` that will
   authenticate you in the `npm` registry.

- This action is empty by default and gets called on all places where packages
  are installed
- To authenticate you would need to configure some repository secrets, depending
  on your auth approach. All the secrets will be accessible as environment
  variables, and not through the GitHub `${{ secrets }}`. This is done to
  overcome a limitation in GitHub reusable actions: they can't inherit secrets
  but do inherit environment variables.
  - `SECRET_NPM_REGISTRY_AUTH_TOKEN` – for this to have a value you must create
    a secret in your repository settings called `NPM_REGISTRY_AUTH_TOKEN`
  - `SECRET_NPM_REGISTRY_USER` – for this to have a value you must create a
    secret in your repository settings called `NPM_REGISTRY_USER`
  - `SECRET_NPM_REGISTRY_PASSWORD` – for this to have a value you must create a
    secret in your repository settings called `NPM_REGISTRY_PASSWORD`

6. If you are publishing to a private registry set this at the top of the
   [`<repo root>/.npmrc`](./.npmrc).

</details>

### If you want to automatically deploy applications

<details>
<summary>Expand to see steps for setting up automatic application deployment</summary>

1. Follow the first 3 steps from the instructions for
   [automatic `npm` publishing](#automatic-npm-publishing)
2. If you use Slack and you want to get message to a channel of your choice, set
   up a GitHub repository secret named `SLACK_WEBHOOK_URL` with a webhook
   generated from your slack admin
3. Open
   [`<repo root>/.github/workflows/_repo-deploy-single-project-on-push.yaml`](./workflows/_repo-deploy-single-project-on-push.yaml)
   and copy the `example` job there, after which customize the steps to match
   the specifics of your app deployment

</details>

<p> </p>

[⬆️ Back to top nav ⬆️](#breakproof-nav)

<p> </p>

<a name="best-practices-list"></a>

# 🏆 List of Best Practices

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        badge | details                                                                                                                                                                                                                                                   |
| -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             <picture><img src="https://custom-icon-badges.demolab.com/badge/code_generator-E0DDCE?logo=terminal&logoColor=ffffff&labelColor=000000&style=flat-square" valign="middle" style="visibility:visible"/></picture> | **generate** all required **files for a new project** via interactive CLI step-by-step wizard                                                                                                                                                             |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   <picture><img src="https://custom-icon-badges.demolab.com/badge/tests-E0DDCE?logo=check-circle&logoColor=29C82E&labelColor=w