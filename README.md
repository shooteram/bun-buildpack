# Bun Buildpack for Scalingo

A Scalingo buildpack that detects and installs dependencies using [Bun](https://bun.sh).

## Detection

This buildpack will be applied to your project if a `bun.lockb` file exists in the project root.
