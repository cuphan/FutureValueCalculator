pipeline {
  agent { node { label 'linux-master' } }

  environment {
    dotnet = "/usr/bin/dotnet"
  }

  stages {
    stage("Restore") {
      steps {
        sh "$dotnet restore"
      }
    }

    stage('Restore PR') {
      agent { node { label 'linux-slave-1' } }
      when {
        branch "PR-*"
      }
      steps {
        sh "$dotnet restore"
      }
    }

    stage("Clean") {
      steps {
        sh "$dotnet clean"
      }
    }

    stage("Clean PR") {
      agent { node { label 'linux-slave-1' } }
      when {
        branch "PR-*"
      }
      steps {
        sh "$dotnet clean"
      }
    }

    stage("Build") {
      steps {
        sh "$dotnet build"
      }
    }

    stage("Build PR") {
      agent { node { label 'linux-slave-1' } }
      when {
        branch "PR-*"
      }
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