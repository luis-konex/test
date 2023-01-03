pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git branch: "main",
          credentialsId: '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',
          url: 'https://github.com/luis-konex/test.git'
      }
    }

    stage('Upload to S3') {
        steps{
            script {

                dir(''){

                    pwd(); //Log current directory

                    withAWS(region:'us-east-1',credentials:'AKIA6CPAK37JLRLOGBHF') {

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