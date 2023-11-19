# Contributing

Thank you for considering contributing to IPNN!
Please read these guidelines before submitting a pull request or opening an issue.

## Specification guidelines

Specification should be written in markdown and should follow [markdownlint](https://github.com/DavidAnson/markdownlint) style and follow the convention below.

### File Naming Convention

The file name for an IIP should adhere to the following convention:
- The file should be prepended with `iip` followed by two digits or more digits, where a single-digit number is always prepended with a 0.
- Examples:
  - iip-01.md
  - iip-02.md
  - ...
  - iip-100.md
  - iip-121.md
  - iip-xx.md

## IIP Structure

The structure of an IIP document is designed to provide a clear and organized presentation of the proposal. Each IIP consists of the following sections:

### Header

The header will be formatted using YAML metadata block. The header should contain the following fields:

- `iip`: The IIP number is a unique identifier for the proposal and is placed at the beginning of the document, following the format `IIP-XX`, where XX is the assigned number.

- `title`: The title section should succinctly convey the main idea or purpose of the proposal.

- `status`: Status can be `draft` or `standard`

- `type`: Type can be `optional` or `required`

- `author`: The author section should contain the list of authors (comma separated), which should be formatted as `name/github username <email>`.
  - Example: `eznix86 <myemail@private.com>`
  - Example: `eznix86` where email is optional

- `created`: The date the IIP was created

Example:

```markdown
---
iip: 0
title: IIP title
status: draft, standard
type: optional, required
author: name <email@example.com>, name2 <email@example2.com>
created: 2023-07-10
---
```

### Abstract

The abstract section provides a brief overview of the proposal, including its purpose and significance.

### Motivation

This section is optional. The motivation section should include a description of any nontrivial problems the IIP solves. It should not describe how the IIP solves those problems, unless it is not immediately obvious. It should not describe why the IIP should be made into a standard, unless it is not immediately obvious.

### Specification

The Specification section should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations.

It is recommended to follow RFC 2119 and RFC 8170. Do not remove the key word definitions if RFC 2119 and RFC 8170 are followed.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

### Additional Section

This section is optional. An additional section may include various subsections. One such subsection is the "Security Considerations" section, addressing potential security implications of the proposed changes.

## Template

A template for IIPs can be found [here](./iip-template.md)

## Commit guidelines

Please follow these guidelines when committing changes to Redvin:

- Each commit should represent a single, atomic change to the codebase.
  Avoid making multiple unrelated changes in a single commit.
- Use the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) format for commit messages and Pull Request titles.

List of conventional commit [types](https://github.com/commitizen/conventional-commit-types/blob/master/index.json):

| Types    | Description                                                                               |
| -------- | ------------------------------------------------------------------------------------------|
| fix      | A big fix (this will ultimately create a breaking change to the current specification)    |
| feat     | A new specification                                                                       |
| ci       | Changes to our CI configuration files and scripts                                         |
| refactor | A rewrite to the documentation that neither fixes the specification nor adds a feature    |
| chore    | Other changes that don't modify the core specification, can include a typo for example    |

_fix_: The footer should contain a breaking change description with the `BREAKING CHANGE:` prefix if the commit introduces a breaking change. A breaking change can be part of commits of any type. A fix will be throughly reviewed and may be rejected.