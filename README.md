<p align="center">
  <img src="/demo.png" alt="Actualbudget" />
</p>

## Getting Started

## Desktop-only fork: run the app locally (no server)

This fork is trimmed to be desktop-first. The sync server was archived to
`archive/sync-server-museum` and is not required to run the desktop app.

Quick start (macOS / Linux):

1. Clone the repo:

```bash
git clone https://github.com/<your-user>/factual.git
cd factual
```

2. Install Yarn 4 (Berry) if you don't have it and bootstrap the workspace:

```bash
# Install Yarn (if needed)
npm install -g yarn
# From repo root
yarn
```

3. Start the desktop app in development (this builds the core lib and runs
   the Electron app):

```bash
yarn start:desktop
```

Notes and troubleshooting:

- The archived sync server is preserved in `archive/sync-server-museum` for
  historical reference. It is not part of the active workspace and does not
  need to be built or run for the desktop app to work.
- If you want a completely clean lockfile without any archived workspace
  references, run `yarn` locally to regenerate `yarn.lock` after moving the
  server out of `packages/` (this repo already stores the server under
  `archive/` so your local `yarn` run will remove workspace resolutions
  referring to it).
- If `yarn start:desktop` fails due to missing native deps or Electron
  rebuilds, run `yarn rebuild-electron` and try again.
- To run the packaged desktop release, use `yarn package-electron` (see
  `bin/package-electron` for details); packaging no longer builds the
  archived sync-server.

If you want, I can also add a minimal CONTRIBUTING-DESKTOP.md with a
small checklist for contributors working on the desktop-only experience.

Actual is a local-first personal finance tool. It is 100% free and open-source, written in NodeJS, it has a synchronization element so that all your changes can move between devices without any heavy lifting.

If you are interested in contributing, or want to know how development works, see our [contributing](https://actualbudget.org/docs/contributing/) document we would love to have you.

Want to say thanks? Click the ⭐ at the top of the page.

## Key Links

- Actual [discord](https://discord.gg/pRYNYr4W5A) community.
- Actual [Community Documentation](https://actualbudget.org/docs)
- [Frequently asked questions](https://actualbudget.org/docs/faq)

## Installation

There are four ways to deploy Actual:

1. One-click deployment [via PikaPods](https://www.pikapods.com/pods?run=actual) (~1.40 $/month) - recommended for non-technical users
1. Managed hosting [via Fly.io](https://actualbudget.org/docs/install/fly) (~1.50 $/month)
1. Self-hosted by using [a Docker image](https://actualbudget.org/docs/install/docker)
1. Local-only apps - [downloadable Windows, Mac and Linux apps](https://actualbudget.org/download/) you can run on your device

Learn more in the [installation instructions docs](https://actualbudget.org/docs/install/).

## Ready to Start Budgeting?

Read about [Envelope budgeting](https://actualbudget.org/docs/getting-started/envelope-budgeting) to know more about the idea behind Actual Budget.

### Are you new to budgeting or want to start fresh?

Check out the community's [Starting Fresh](https://actualbudget.org/docs/getting-started/starting-fresh) guide so you can quickly get up and running!

### Are you migrating from other budgeting apps?

Check out the community's [Migration](https://actualbudget.org/docs/migration/) guide to start jumping on the Actual Budget train!

## Documentation

We have a wide range of documentation on how to use Actual, this is all available in our [Community Documentation](https://actualbudget.org/docs), this includes topics on Budgeting, Account Management, Tips & Tricks and some documentation for developers.

## Contributing

Actual is a community driven product. Learn more about [contributing to Actual](https://actualbudget.org/docs/contributing/).

### Code structure

The Actual app is split up into a few packages:

- loot-core - The core application that runs on any platform
- desktop-client - The desktop UI
- desktop-electron - The desktop app
- sync-server - (archived in this fork) the sync server has been moved to `archive/sync-server-museum` and is not part of the desktop-only build

More information on the project structure is available in our [community documentation](https://actualbudget.org/docs/contributing/project-details).

### Feature Requests

Current feature requests can be seen [here](https://github.com/actualbudget/actual/issues?q=is%3Aissue+label%3A%22needs+votes%22+sort%3Areactions-%2B1-desc).
Vote for your favorite requests by reacting :+1: to the top comment of the request.

To add new feature requests, open a new Issue of the "Feature Request" type.

### Translation

Make Actual Budget accessible to more people by helping with the [Internationalization](https://actualbudget.org/docs/contributing/i18n/) of Actual. We are using a crowd sourcing tool to manage the translations, see our [Weblate Project](https://hosted.weblate.org/projects/actualbudget/). Weblate proudly supports open-source software projects through their [Libre plan](https://weblate.org/en/hosting/#libre).

<a href="https://hosted.weblate.org/engage/actualbudget/">
<img src="https://hosted.weblate.org/widget/actualbudget/actual/287x66-grey.png" alt="Translation status" />
</a>

## Repo Activity

![Alt](https://repobeats.axiom.co/api/embed/e20537dd8b74956f86736726ccfbc6f0565bec22.svg 'Repobeats analytics image')

## Sponsors

Thanks to our wonderful sponsors who make Actual Budget possible!

<a href="https://www.netlify.com"> <img src="https://www.netlify.com/v3/img/components/netlify-color-accent.svg" alt="Deploys by Netlify" /> </a>
