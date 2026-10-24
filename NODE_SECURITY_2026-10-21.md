# Node.js security update (2026-10-21)

Official advisory: https://nodejs.org/en/blog/vulnerability/october-2026-security-releases

Fixed versions are 22.23.4, 24.22.1 and 26.12.1. Pin explicit Node build/runtime settings, move EOL Node 18/20 to 22, and preserve existing dependencies and application behavior. Exact production patch versions remain unverified. A package engines declaration is not proof of the deployed runtime.

Validation: JSON manifests and diff whitespace checked locally. Application dependency installation, typecheck, test/build, native Docker compatibility and startup remain pending (Mac disk capacity is limited); existing PR CI must pass before merge. This is a draft, not a completed production repair.

For Node 20 to 22 or Alpine upgrades, check native modules and TLS/OpenSSL in the actual target image. Before deployment record each target service, current image/revision and traffic, test a no-traffic candidate where available, then use the existing approval/promotion path. Roll back to the recorded previous revision on failure; that rollback restores the old security risk. No production deploy, auth expansion, new keys, database change or auto-merge is included.

## 2026-10-24 validation follow-up

Reapplied only the Node settings to current source a141e8d2468333024872f62f38d753c2e3a1f049 after the original PR history diverged. The isolated Node 22.23.4 VitePress documentation build passed. The package resolution graph and application/document content are unchanged. The documentation workflow still has its existing `master` trigger; changing the renamed branch's publication policy is outside this security fix. This is a build-time Node update, not evidence of any deployed Node server runtime.
