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

    stage("Build") {
      steps {
        sh "$dotnet build"
      }
    }

    stage('Deploy Test') {
      when {
        branch "test"
      }
      steps {
        script {
          echo "Run deploy for Testing environment"
        }
      }
    }

    stage('Deploy Production') {
      when {
        branch "main"
      }
      steps {
        script {
          echo "Run deploy for Production environment"
        }
      }
    }
  }
}