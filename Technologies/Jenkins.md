---
tags:
  - technologies
  - web
date: 2023-09-1
---
- Open source automation server.
- Used for `Continuous Integration/Continuous Deployment (CI/CD)`.
- Allows:
	- automation of software build, test, and deployment pipelines.
	- integrates with Git, [[Docker]], [[Kubernetes]] and [[Ansible]].
- Written in Java.
# Concepts

- `Job/Project`: runnable task (freestyle, pipeline, multibranch, etc..).
- `Pipeline`: script defining stages of CI/CD.
- `Build Node`: system where jobs are executed (master or agent).
- `Executor`: thread on a node that runs a job.
- `Workspace`: directory where builds run.
- `Artifact`: output of build.
- `Plugin`: extend Jenkins capabilities.
# Jenkinsfile

- Tells Jenkins how to build, test and deploy apps.
	- blueprint for CI/CD pipeline.
- Defines:
	- agent/node to use.
	- stages of pipeline
	- actual commands to execute
	- potential creds, environment variables, post-job actions, notifications
- Uses `Groovy` - scripting language.
- Used to:
	- define scripted pipelines
	- power declarative pipelines
	- write advanced logic in Jenkinsfiles
- Two pipeline syntaxes in Jenkins:
	- `Declarative` - structured/readable
	- `Scripted` - pure Groovy
- Example declarative:

```groovy
pipeline {
  agent any

  environment {
    BUILD_ENV = 'production'
  }

  stages {
    stage('Build') {
      steps {
        sh 'make build'
      }
    }
    stage('Test') {
      steps {
        sh 'make test'
      }
    }
  }

  post {
    always {
      echo 'This runs regardless of success/failure.'
    }
  }
}
```

- An example scripted:

```groovy
node {
  def branches = ['main', 'dev']

  for (b in branches) {
    stage("Build ${b}") {
      echo "Building branch: ${b}"
      sh "make build BRANCH=${b}"
    }
  }

  stage('Test') {
    try {
      sh 'make test'
    } catch (err) {
      echo "Tests failed: ${err}"
    }
  }
}
```