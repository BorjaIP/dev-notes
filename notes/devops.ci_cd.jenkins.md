---
id: j3fw4ldb0j01jdqefl42iuo
title: Jenkins
desc: ''
updated: 1655320412473
created: 1655320362766
---

- Select agent to run a Pipeline.
  
```bash
{
    node {
        label 'nodejs'
    }
}
```

## Variables

```groovy
# Only works on multibranch pipeline
env.BRANCH_NAME
# Workaround
\\...
stage('Test') {
        steps {
            script {
                branchName = sh(label: 'getBranchName', returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
                println branchName
            }   
        }
      } 
\\...
```