# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] (2023-07-08)

### Fixed
- Support for `\n` sequences in message `text` input ([#1]).

## [1.0.2] (2023-02-07)

### Changed
- Switched from the deprecated `set-output` command to the new `$GITHUB_OUTPUT` environment file.

## [1.0.1] (2022-07-08)

### Added
- Option to select the host environment when running manual tests.

### Changed
- Disabled curl's progress meter for cleaner output.

## [1.0.0] (2022-06-26)

### Added
- Support for sending basic Slack messages.
- Support for sending Slack messages with custom channel, icon and username.
- Support for Slack messages with attachments.
- Automated tests on all supported GitHub-hosted runners (`macos-*`, `ubuntu-*` and `windows-*`).

[unreleased]: https://github.com/pcolby/post-to-slack/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/pcolby/post-to-slack/releases/tag/v1.1.0
[1.0.2]: https://github.com/pcolby/post-to-slack/releases/tag/v1.0.2
[1.0.1]: https://github.com/pcolby/post-to-slack/releases/tag/v1.0.1
[1.0.0]: https://github.com/pcolby/post-to-slack/releases/tag/v1.0.0

[#1]: https://github.com/pcolby/post-to-slack/issues/1 "New Line Character Doesn't Work"
