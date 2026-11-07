# Contributing to Git Gud Gym

Thanks for helping. This guide applies to every repository in the
[Git-Gud-Gym](https://github.com/Git-Gud-Gym) organization; each repo's README covers how to build it.

## Where things live

| You want to… | Go to |
|---|---|
| Report a bug in the app, library or overlay | [launcher issues](https://github.com/Git-Gud-Gym/launcher/issues/new/choose) |
| Report a bug in a specific game | that game's `module-<game>` repo |
| Request a new game, or 👍 an existing request | [registry](https://github.com/Git-Gud-Gym/registry/issues/new?template=game_request.yml) |
| Add support for a game | [SDK: Adding a game](https://github.com/Git-Gud-Gym/sdk/blob/main/docs/ADDING_A_GAME.md) |
| Improve the trainer core (immortality, falls, stats) | [sdk](https://github.com/Git-Gud-Gym/sdk) |
| Improve the website or docs | [git-gud-gym.github.io](https://github.com/Git-Gud-Gym/git-gud-gym.github.io) |
| Ask a question | [Discussions](https://github.com/Git-Gud-Gym/launcher/discussions) |

For bug reports, press <kbd>F8</kbd> in game first and attach `gitgudgym.log` (the *Log* button on
the game's page in the app).

## Pull requests

1. Fork, then branch from `main`.
2. Keep each PR focused: one feature or fix.
3. Match the surrounding style. C++ is formatted with the repo's `.clang-format`.
4. CI must pass. New compiler warnings at `/W4` count as failures.
5. For gameplay changes, say which game, which patch, and what you tested in game.
6. Add a line to the repo's `CHANGELOG.md` if users will notice the change.

## How the pieces fit

```
sdk  ──(FetchContent, pinned tag)──►  module-<game>  ──(release)──►  registry  ──►  catalog.json
 │                                                                                    │
 └──(contract headers)──►  launcher  ◄───────────── reads the catalog ────────────────┘
```

- **SDK changes** that touch the shared-memory contract are breaking: they need a major version
  and a new mapping name, and the launcher and modules update together.
- **Modules and the launcher** release independently with `vX.Y.Z` tags. Each repo's release
  workflow builds, packages and publishes.
- **The registry** lists only repos inside this organization, because the launcher runs as
  administrator.

## Ground rules

- **Offline and single-player only.** We never help bypass anti-cheat for online play. Modules must
  list the game's anti-cheat processes so the launcher refuses to attach while they run.
- **No publisher assets.** No game art, logos or game files in any repo or on the website.
- **Be kind.** See the [Code of Conduct](CODE_OF_CONDUCT.md).
