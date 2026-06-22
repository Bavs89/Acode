# Codebase task proposals

## 1) Typo fix
- **Task:** Correct the typo `enviroment` to `environment` in the terminal installation progress log.
- **Why:** User-facing logs should be spelled correctly for professionalism and searchability.
- **Location:** `src/plugins/terminal/www/Terminal.js` (log message: `"⚙️  Updating sandbox enviroment..."`).

## 2) Bug fix
- **Task:** Make `readAsset` steps in `startAxs()` deterministic by awaiting file-write completion before starting the shell script.
- **Why:** `readAsset(...)` callbacks are fired asynchronously, but the code currently proceeds to `Executor.start("sh", ...)` without ensuring all scripts have actually been written. This can lead to race conditions where `init-sandbox.sh` or wrapper scripts are not ready when execution starts.
- **Location:** `src/plugins/terminal/www/Terminal.js` in `startAxs()` (both `installing` and non-installing branches).

## 3) Code comment/documentation discrepancy
- **Task:** Update the JSDoc return contract for `startAxs()` to match runtime behavior (or refactor code to match docs).
- **Why:** The doc says `@returns {Promise<boolean>}` but also mentions `void if not installing`, which is contradictory and confusing for integrators and type tooling.
- **Location:** `src/plugins/terminal/www/Terminal.js` JSDoc above `startAxs()`.

## 4) Test improvement
- **Task:** Strengthen the `Error handling` sanity test so it fails if no error is thrown.
- **Why:** Current test only asserts inside `catch`, so if the throw is accidentally removed, the test still passes (false positive).
- **Location:** `src/test/sanity.tests.js` (`Error handling` test case).
