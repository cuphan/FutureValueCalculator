pipeline {
  agent { node { label 'linux-master' } }

  environment {
    dotnet = "/usr/bin/dotnet"
  }

  stages {
    stage("Restore") {
      when {
        not {
          branch "PR-*"
        }
      }
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
      when {
        not {
          branch "PR-*"
        }
      }
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
      when {
        not {
          anyOf {
            branch "PR-*";
            branch "test"
          }
        }
      }
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