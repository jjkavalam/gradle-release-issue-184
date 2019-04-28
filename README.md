# What is this branch about ?

The `good-case-branch` demonstrates that if the `gradle.properties` is just one level
deep from the root of the git repo, then the plugin does not report that it failed
while trying to roll back changes to it.

Example:

```
PS C:\jjkavalam\gradle-release-issue-184> .\gradlew release
> Task :project:initScmAdapter FAILED

> Task :release FAILED
Release process failed, reverting back any changes made by Release Plugin.

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':project:initScmAdapter'.
> Current Git branch is "the-good-case" and not "master".

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 2s
1 actionable task: 1 executed
```