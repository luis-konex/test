pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git branch: "main",
          // credentialsId: 'cfd6c76a-406c-4a8f-af8c-13d907ef0d4b',
          url: 'git@github.com:spinningops/website-pipeline-demo.git'
      }
    }

    stage('Upload to S3') {
        steps{
            script {

                dir(''){

                    pwd(); //Log current directory

                    withAWS(region:'us-east-1',credentials:'Tt0qhLimt3o8d/m56IgHhmuqXxeBebe5yuxNJMzx') {

                        def identity=awsIdentity();//Log AWS credentials

                        // Upload files from working directory '' in your project workspace
                        s3Upload(bucket:"qa.neat.red", workingDir:'', includePathPattern:'**/*');
                        // invalidate CloudFront distribution
                        cfInvalidate(distribution:'E1DLLYQ06DZX5X', paths:['/*'])
                    }

                };
            }
        }
    }

  }

}