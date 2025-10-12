# DotNet useful tips

## Table of contents

- [Aspire](#aspire)
  - [Install](#installation)

# Aspire

[Docs](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-overview)

## Installation

Install templates:

```bash
dotnet new install Aspire.ProjectTemplates
```

Install CLI:

```bash
curl -sSL https://aspire.dev/install.sh -o aspire-install.sh

sh aspire-install.sh
```

For MAC need to register PATH so command line will know what's aspire:

1. In the user's root/home directory find file .zprofile
2. Add next lines to the file:

```bash
# DotNet Aspire
export PATH="/Users/<username>/.aspire/bin:$PATH"
```

3. restart command line
