# Vendored Prisma schema engine

This folder holds Prisma's `schema-engine` binary so the backend can be
installed and migrated on machines that cannot reach `binaries.prisma.sh`.
Prisma normally downloads this file during `pnpm install` (in the
`@prisma/engines` install script) and needs it for `prisma migrate deploy`.

| | |
|---|---|
| File | `schema-engine-debian-openssl-3.0.x` |
| Prisma version | `prisma` / `@prisma/client` 7.9.1 |
| Engine build | `e922089b7d7502aff4249d5da3420f6fa55fc6ad` |
| Platform | `debian-openssl-3.0.x` (Linux x86-64 with OpenSSL 3, e.g. Ubuntu 22.04/24.04) |
| Source | `https://binaries.prisma.sh/all_commits/e922089b7d7502aff4249d5da3420f6fa55fc6ad/debian-openssl-3.0.x/schema-engine.gz` |
| SHA-256 (uncompressed) | `6a516632d085842ec5a31a6a9e81f39feea3963ec4574f54f62886e4403f6b53` |
| License | Apache-2.0, see `LICENSE-prisma-engines` (copied from `@prisma/engines`) |

Verify the file before use:

```bash
echo "6a516632d085842ec5a31a6a9e81f39feea3963ec4574f54f62886e4403f6b53  schema-engine-debian-openssl-3.0.x" | sha256sum -c -
```

## Usage

Point Prisma at the file with an **absolute** path before installing. pnpm
runs install scripts from inside each package's folder, so a relative path
would resolve to the wrong place. From the repository root:

```bash
export PRISMA_SCHEMA_ENGINE_BINARY="$PWD/packages/hoppscotch-backend/prisma-engines/schema-engine-debian-openssl-3.0.x"
pnpm install --frozen-lockfile
cd packages/hoppscotch-backend && pnpm exec prisma migrate deploy
```

## Updating

This binary only matches Prisma 7.9.1. When `prisma` is upgraded, replace it
with the build named by `@prisma/engines-version` for the new version
(`https://binaries.prisma.sh/all_commits/<hash>/debian-openssl-3.0.x/schema-engine.gz`),
check it against the published `.sha256` files, and update this README.
