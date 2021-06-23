pipeline {
  agent { node { label 'linux-slave-1' } }

  environment {
    dotnet = "/usr/bin/dotnet"
  }

  options {
    buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
    disableConcurrentBuilds()
    ansiColor('xterm')
  }

  stages {
    stage("Restore") {
      steps {
        sh "$dotnet restore"
      }
    }

    stage("Clean") {
      steps {
        sh "$dotnet clean"
      }
    }

    stage("Build PR") {
      when {
        branch "PR-*"
      }
      steps {
        sh "$dotnet build"
      }
    }

    stage('Build Test') {
      when {
        branch "test"
      }
      steps {
        script {
          sh "$dotnet build -c Test"
        }
      }
    }

    stage('Build Production') {
      when {
        branch "main"
      }
      steps {
        script {
          sh "$dotnet build -c Production"
        }
      }
    }
  }
}