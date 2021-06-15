pipeline {
  agent { node { label 'windows-slave1' } }

  //environment {
  //  dotnet = '/usr/bin/dotnet'
  //}

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
        bat "dotnet restore"
      }
    }

    stage('Clean') {
      steps {
        bat 'dotnet clean'
      }
    }

    stage('Build') {
      steps {
        bat 'dotnet build --configuration Release'
      }
    }

    // stage('Pack') {
    //   steps {
    //     sh 'dotnet pack --no-build --output nupkgs'
    //   }
    // }

    // stage('Publish') {
    //   steps {
    //     sh "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
    //   }
    // }
  }
}
