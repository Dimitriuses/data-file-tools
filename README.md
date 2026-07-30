# data-file-tools

![Angular 12.0.5](https://img.shields.io/badge/Angular-12.0.5-dd0031)
![TypeScript 4.2](https://img.shields.io/badge/TypeScript-4.2-3178c6)
![Licence MIT](https://img.shields.io/badge/licence-MIT-blue)
![Status: archived](https://img.shields.io/badge/status-archived-lightgrey)

**An empty Angular project. Nothing was ever built in it.**

This repository contains one commit, made on 16 March 2022, consisting of the
untouched output of `ng new`. There is no application here — the page it serves
is the Angular CLI's own welcome screen. It is kept public because deleting it
would hide a real and fairly common thing: a project that was set up and then
never started.

## Status and history

The whole repository has a lifetime of **twenty-five minutes**:

| | |
|---|---|
| Repository created on GitHub | 2022-03-16 15:50:07 UTC |
| The one and only commit — `create new project` | 2022-03-16 16:14:58 UTC |
| Pushed | 2022-03-16 16:15:07 UTC — **nine seconds later** |
| Touched again | never |

No second commit, no branch, no issue, and — unusually for a 2022 repository with
a committed lockfile — **not a single pull request in its history**, Dependabot
included.

The name is the only surviving statement of intent. Something to do with data
files was planned; **what those tools were meant to do is not recorded anywhere
in the repository**, and this README does not guess. Even the `title` property in
`app.component.ts` is not a statement of intent — the CLI generates it from the
directory name.

## What is actually in this repository

All **26 tracked files are Angular CLI 12.0.5 scaffolding, unmodified**. That is
not an impression from reading them; it was measured, because it is the only
claim this README makes and a wrong one would be worthless.

The method: download `@schematics/angular@12.0.5` from npm, render its templates
with the same template engine and the same variables the CLI passes them
(`ng new data-file-tools`, answering *routing: yes* and *stylesheet: SCSS*, with
`strict` at its v12 default of `true`), then compare each result against the
committed file.

| Files | Result |
|---|---|
| 23 templated files | **byte-identical** to the rendered templates |
| `angular.json` | **deep-equal** to the object the application schematic builds in code — it is assembled programmatically, not templated |
| `package.json` | differs by **exactly one line**: `"@angular-devkit/build-angular": "~12.0.5"`, which the CLI inserts into `devDependencies` after templating |
| `package-lock.json` | npm's own output; its `name`/`version` match `package.json`, and every dependency declared there resolves in it at a matching version |

The only systematic difference is line endings: this is a Windows checkout, so
every non-empty text file in it is CRLF where the templates are LF. That is an
artifact of `git` on Windows, not an edit, and the comparison above normalises
it.

So the 509-line `src/app/app.component.html` — by far the largest hand-editable
file here — is the CLI's stock welcome page, rockets and all. **The repository
contains no lines written by its author.**

## Does it still run?

Yes, and this was verified in July 2026 on Node 22.20 rather than assumed — in a
scratch copy, since nothing in this repository has been modified.

```
npm ci                                  1308 packages, no native rebuild, no peer conflicts
ng build                                246.69 kB initial, 0 errors, 0 warnings
ng test --watch=false                   Executed 3 of 3 SUCCESS
```

**One environment variable is required on any modern Node:**

```bash
export NODE_OPTIONS=--openssl-legacy-provider   # PowerShell: $env:NODE_OPTIONS='--openssl-legacy-provider'
npm ci
npx ng serve        # http://localhost:4200
```

Without it the build dies with `ERR_OSSL_EVP_UNSUPPORTED` — webpack asking
OpenSSL 3 for md4, which OpenSSL 3 no longer provides. It is a toolchain
incompatibility with a Node released after this project, not a fault in the
project. Nothing else is needed: the lockfile pins `sass@1.32.12`, which is
dart-sass, so there is no native module to compile against a dead Node ABI —
the usual reason a 2019–2022 front-end cannot be installed today.

The three generated unit tests pass. They pass *because* the template was never
edited — the stock spec asserts on the stock welcome page, and both are still
stock. It is the one benefit of having written nothing.

## Layout

```
src/
  app/          app.component.{ts,html,scss,spec.ts}, app.module.ts, app-routing.module.ts
  environments/ environment.ts, environment.prod.ts
  index.html, main.ts, polyfills.ts, styles.scss, test.ts, favicon.ico
angular.json, package.json, package-lock.json, karma.conf.js, tsconfig*.json
```

`app-routing.module.ts` declares `const routes: Routes = []` — routing was
enabled at generation time and never used.

## Known limitations

- **There is no application.** Every heading above describes scaffolding. Nothing
  can be demonstrated, because nothing was written.
- **No live demo, deliberately.** The other archived web projects here link to a
  running page; this one does not, and publishing the Angular welcome screen
  under this repository's name would advertise someone else's page as the work.
- **The name promises a program that does not exist.** `data-file-tools` describes
  an intention, and the repository is the point at which that intention stopped.
- **The commit message is `create new project`, and it is accurate but useless.**
  Nothing records what was planned, so the intent could not be recovered later —
  which is the actual lesson in this repository.
- **`@angular/animations` and `@angular/forms` are declared and imported by
  nothing.** That is `ng new`'s default dependency set, not a decision made here.
- **The toolchain is end-of-life.** Angular 12 left long-term support in November
  2022; `lockfileVersion` is 1 (npm 6). The dependency tree carries the
  vulnerability count you would expect of a 2022 build toolchain. It is archived,
  not maintained, and none of it is reachable at runtime.

## Retrospective

Three things are visibly wrong here, and only the first is really about code.

1. **Publishing an empty scaffold is a decision, and it was the wrong one.** The
   cost of `ng new` is thirty seconds; the cost of pushing it to a public profile
   is a permanent entry that reads as abandoned work. Generating a project and
   pushing it nine seconds after the first commit means the repository existed
   before there was anything to put in it. Work locally first, and create the
   remote when there is something to show.

2. **A repository is not a plan.** No note, no issue, no TODO — so four years
   later the intent is unrecoverable even by its author. One sentence in the
   README at generation time would have preserved it, and that sentence is the
   cheapest artifact in software.

3. **It was never revisited.** Not to continue it, not to delete it, not to add
   a line saying it was abandoned. Reviewing your own public profile
   occasionally is part of maintaining it; this file is that review, arriving
   four years late.

There is no "before and after" section in this README because there is no bug to
fix and nothing to rebuild. Saying so is more useful than manufacturing a story.

## Licence

[MIT](LICENSE). Note that the licence covers essentially nothing original — all
of the code is Angular CLI scaffolding, itself MIT-licensed by Google LLC.
