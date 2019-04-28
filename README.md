# What is this repo about ?

This repo is related to my (@jjkavalam) comment in https://github.com/researchgate/gradle-release/issues/184

Reverting any potential changes to `gradle.properties` is a common rollback action taken by the gradle-release plugin.

However, the plugin (v2.8.0 in this case) seems to get into trouble if the `gradle.properties` is two or more level 
deep from the root of the git repository.

# How to reproduce issue ?

1. Clone this repository
2. cd <root>/project
3. run `./gradlew release`

Notice: `Running [git, checkout, gradle.properties] produced an error: [error: pathspec 'gradle.properties' did not match any file(s) known to git.]`

```
PS C:\jjkavalam\gradle-release-issue-184\project> .\gradlew release                                                                                      
                                                                                                                                                         
> Task :project:checkoutMergeToReleaseBranch FAILED                                                                                                      
Running [git, checkout, release] produced an error: [error: pathspec 'release' did not match any file(s) known to git.]                                  
                                                                                                                                                         
> Task :release                                                                                                                                          
Release process failed, reverting back any changes made by Release Plugin.                                                                               
Running [git, checkout, gradle.properties] produced an error: [error: pathspec 'gradle.properties' did not match any file(s) known to git.]              
                                                                                                                                                         
> Task :release FAILED                                                                                                                                   
                                                                                                                                                         
FAILURE: Build failed with an exception.                                                                                                                 
                                                                                                                                                         
* What went wrong:                                                                                                                                       
Execution failed for task ':project:checkoutMergeToReleaseBranch'.                                                                                       
> Failed to run [git checkout release] - [][error: pathspec 'release' did not match any file(s) known to git.                                            
  ]                                                                                                                                                      
                                                                                                                                                         
* Try:                                                                                                                                                   
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.     
                                                                                                                                                         
* Get more help at https://help.gradle.org                                                                                                               
                                                                                                                                                         
BUILD FAILED in 10s                                                                                                                                      
1 actionable task: 1 executed                                                                                                                           
```

# Guessing the cause

The `the-good-case` branch of this repository has the same gradle project, but instead of `<root>/project/` it is 
located at `<root>/`. In this case, there is no complaint about a failed checkout of gradle.properties.
