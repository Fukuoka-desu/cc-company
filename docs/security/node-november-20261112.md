# Node November security patch

Starting source `6ab8d34050eb2a4c37f23f58826f6ea6ac5252a9`. Update the existing22/24 patch floors to22.23.5/24.22.3
from the official2026-11-11 security release, keeping OS variants, package
resolutions, application behavior, permissions and data unchanged.

Sources: https://nodejs.org/en/blog/vulnerability/november-2026-security-releases
and https://github.com/nodejs/node/releases/tag/v22.23.5 . Some changelog CVEs
affect24/26 only; do not count them as affected22.x. Conditions and real runtime
are separate from pins. Existing Node22.23.4 Mac tests are compatibility only.

Before publication: execute existing repository test/build/lint gates where
available, verify exact runtime-only diff and lock metadata, review in this
session, re-read owner/PR/head, normal push and Draft PR only. No Ready/merge/
deploy, daemon/VM, real notifications, DB writes, auth/security configuration or
new host SDK. CI/live image/process/device and external-service gaps stay open.
Browser/device behavior and support matrix are unchanged; this patch does not
claim new mobile/browser/PWA acceptance. Rollback to the old image restores old
runtime risk; production release and rollback require separate approval.
