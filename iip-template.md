# IIP Guide

## Overview

This guide outlines the structure and key elements of an IIP document, providing a template for authors to use when submitting proposals. Each IIP is identified by a unique number and follows a specific file naming convention.

### File Naming Convention

The file name for an IIP should adhere to the following convention:
- The file is named with two digits, where a single-digit number is always prepended with a 0.
- Examples:
  - 01.md
  - 02.md
  - ...
  - 100.md
  - 121.md

## IIP Structure

The structure of an IIP document is designed to provide a clear and organized presentation of the proposal. Each IIP consists of the following sections:

### IIP Number

The IIP number is a unique identifier for the proposal and is placed at the beginning of the document, following the format `IIP-XX`, where XX is the assigned number.

Example:
```markdown
IIP-XX
======
```

### Title

The title section should succinctly convey the main idea or purpose of the proposal.

Example:
```markdown
[Title]
------
```
### Authors

Example:
```
`author:eznix` `author:kehiy`
```
### Status

Status can be `draft` or `standard` , it prepended to the list of authors 

Example:
```
`standard` `author:eznix86`
```
```
`draft` `author:eznix86`
```

### Introduction/Abstract

The introduction or abstract section provides a brief overview of the proposal, including its purpose and significance.

Example:
```markdown
[Introduction section / Abstract section]
```

### Item Section

The item section is the core of the proposal and may include various subsections. One such subsection is the "Security Considerations" section, addressing potential security implications of the proposed changes.

Example:
```
## [item title section]
[ item content]
```

## Template
```
IIP-XX
======

[Title here]
------------

`draft` `author:[your github username]` `author:[co-author github username]`

[Abstract/Introduction here]

## [Section 1]

[Section 1 Content]

## [Section 2]

[Section 2 Content]

## Security Considerations [Optional]

[Security Considerations Content]