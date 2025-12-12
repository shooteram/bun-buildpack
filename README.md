# Bun Buildpack for Scalingo

A Scalingo buildpack that detects and installs dependencies using [Bun](https://bun.sh), the fast JavaScript runtime and package manager.

## Detection

This buildpack will be applied to your project if either of these files exists in the project root:
- `bun.lockb` (Bun's binary lock format)
- `bun.lock` (Bun's text lock format)

## Configuration

The buildpack will:
1. Install Bun if not already present in the environment
2. Install dependencies using `bun install --frozen-lockfile` when a lock file is present
3. Run the build script defined in `package.json` if it exists
4. Configure runtime environment variables for optimal performance

## Environment Variables

The buildpack sets these default environment variables:
- `PATH`: Includes Bun binary path
- `BUN_INSTALL_CACHE_DIR`: Sets to `/tmp/cache/bun` for package caching
- `NODE_OPTIONS`: Defaults to `--max-old-space-size=2560` for memory management
- `NODE_ENV`: Defaults to `production`

## Usage

Set the buildpack URL in your Scalingo application:

```
BUILDPACK_URL=https://github.com/yourusername/bun-buildpack
```

## Requirements

- Scalingo supports custom buildpacks
- Application must have a `package.json` file
- Dependencies should be managed with Bun (`bun install`)

## Notes

- The buildpack caches Bun installations between deploys for faster builds
- It respects both `bun.lockb` and `bun.lock` files for deterministic installs
- No additional addons are automatically provisioned (removed PostgreSQL addon)
