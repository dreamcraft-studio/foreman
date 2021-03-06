<img align="right" width="300" src="foreman.png" />

# Foreman
[![Actions Status](https://github.com/Roblox/foreman/workflows/CI/badge.svg)](https://github.com/Roblox/foreman/actions?query=workflow%3ACI)
[![Latest Release on crates.io](https://img.shields.io/crates/v/foreman.svg?label=latest%20release)](https://crates.io/crates/foreman)

Foreman is a toolchain manager to help Roblox developers manage their installations of tools like [Rojo](https://github.com/rojo-rbx/rojo), [Remodel](https://github.com/rojo-rbx/remodel), [Tarmac](https://github.com/rojo-rbx/tarmac), and [Selene](https://github.com/Kampfkarren/selene).

Foreman is inspired by [rustup](https://rustup.rs) and [asdf](https://github.com/asdf-vm/asdf).

It's an early prototype, but feedback at this stage is welcome!

## Installation

### GitHub Releases
You can download pre-built Foreman releases for Windows, macOS, and Linux from the [Releases](https://github.com/Roblox/foreman/releases) page.

### GitHub Actions
You can use the official [setup-foreman](https://github.com/rojo-rbx/setup-foreman) action to install Foreman as part of your GitHub Actions workflow.

### From Source
If you have [Rust](https://www.rust-lang.org/) 1.41.0 or newer installed, you can also compile Foreman by installing it from [crates.io](https://crates.io):

```bash
cargo install foreman
```

## Usage
Foreman downloads tools from GitHub and references them by their `user/repo` name, like `Roblox/foreman`.

On first run (try `foreman list`), Foreman will create a `.foreman` directory in your user folder (usually `~/.foreman` on Unix systems, `%USERPROFILE%/.foreman` on Windows).

It's recommended that you **add `~/.foreman/bin` to your `PATH`** to make the tools that Foreman installs for you accessible on your system.

### System Tools
To start using Foreman to manage your system's default tools, create the file `~/.foreman/foreman.toml`.

A Foreman config that lists Rojo could look like:

```toml
[tools]
rojo = { source = "rojo-rbx/rojo", version = "0.5.0" }
```

Run `foreman install` from any directory to have Foreman pick up and install the tools listed in your system's Foreman config.

Now, if you run `rojo` inside of a directory that doesn't specify its own version of Rojo, Foreman will run the most recent 0.5.x release for you!

### Project Tools
Managing a project's tools with Foreman is similar to managing system tools. Just create a `foreman.toml` file in the root of your project.

A Foreman config that lists Remodel might look like this:

```toml
[tools]
remodel = { source = "rojo-rbx/remodel", version = "0.6.1" }
```

Run `foreman install` to tell Foreman to install any new binaries from this config file.

When inside this directory, the `remodel` command will run the latest 0.6.x release of Remodel installed on your system.

### Authentication
To install tools from a private GitHub repository, Foreman supports authenticating with a [Personal Access Token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line).

Use `foreman github-auth` to pass an authentication token to Foreman, or open `~/.foreman/auth.toml` and follow the contained instructions.

## Troubleshooting
Foreman is a work in progress tool and has some known issues. Check out [the issue tracker](https://github.com/Roblox/foreman/issues) for known bugs.

If you have issues with configuration, you can delete `~/.foreman` to delete all cached data and start from scratch. This directory contains all of Foreman's installed tools and configuration.

## License
Foreman is available under the MIT license. See [LICENSE.txt](LICENSE.txt) or <https://opensource.org/licenses/MIT> for details.