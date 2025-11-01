# Install CMake from Source

This composite GitHub Action clones the official Kitware/CMake repository, compiles the latest version from source, and installs it globally.

This is particularly useful when the default CMake version pre-installed on the GitHub Actions runner (e.g., ubuntu-latest, etc.) is older than the minimum version required by your project.

## How to Use

This action runs a hardcoded sequence of steps and requires no inputs.

Example Workflow (`.github/workflows/build.yml`)

```yml
name: Build with CMake

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # 1. Install the latest CMake from source globally
      # This makes the new 'cmake' binary available in the PATH.
      - name: Install latest CMake
        uses: akash1047/install-cmake@v1

      # 2. Checkout your project's code
      # It is best practice to check out your code AFTER installing global tools.
      - name: Checkout Project Code
        uses: actions/checkout@v5

      # 3. Configure and Build your project using the newly installed CMake
      - name: Configure and Build
        run: |
          cmake -B build
          cmake --build build --parallel $(nproc)
```
