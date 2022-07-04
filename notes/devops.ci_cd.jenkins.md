---
id: j3fw4ldb0j01jdqefl42iuo
title: Jenkins
desc: ''
updated: 1656945037672
created: 1655320362766
---

## Scripts

```groovy
script {
    // Trigger by another webhook
    def upstreamCause = currentBuild.rawBuild.getCause(hudson.model.Cause$UpstreamCause)
    UPSTREAM = upstreamCause
    // Get build number from trigger webhook
	def upstreamBuild = Jenkins.instance.getItemByFullName(upstreamCause?.upstreamProject).getBuildByNumber(upstreamCause?.upstreamBuild)
    // Get environment action from trigger webhook
	def upstreamEnv = upstreamBuild.getAction(org.jenkinsci.plugins.workflow.cps.EnvActionImpl).getEnvironment()
	PARENT_ENV = upstreamEnv
    // Trigger by user
    def isStartedByUser = currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause) != null
    // Get all Causes for the current build
    def causes = currentBuild.rawBuild.getCauses()
    println causes
}
```

- Select agent to run a Pipeline.
  
```bash
{
    node {
        label 'nodejs'
    }
}
```

## Variables

- [List of variabales](https://www.perforce.com/manuals/jenkins/Content/P4Jenkins/variable-expansion.html)

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