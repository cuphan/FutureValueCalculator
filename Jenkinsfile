pipeline {
  agent any

  environment {
    dotnet = '/usr/bin/dotnet'
  }

  stages {
    stage('Checkout') {
      steps {
        // git credentialsId: 'userId', url: 'https://github.com/NeelBhatt/SampleCliApp', branch: 'master'
        git url: 'https://github.com/vietphan-billidentity/FutureValueCalculator', branch: 'main'
      }
    }

    stage('Restore PACKAGES') {
      steps {
        // sh "dotnet restore --configfile NuGet.Config"
        sh "dotnet restore"
      }
    }

    stage('Clean') {
      steps {
        sh 'dotnet clean'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build --configuration Release'
      }
    }

    stage('Pack') {
      steps {
        bat 'dotnet pack --no-build --output nupkgs'
      }
    }

    // stage('Publish') {
    //   steps {
    //     bat "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
    //   }
    // }
  }
}