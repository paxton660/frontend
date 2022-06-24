pipeline {
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  containers:
  - name: gcloud
    image: gcr.io/google.com/cloudsdktool/cloud-sdk:slim
    command:
    - cat
    tty: true
"""
    }
  }
  stages {
    stage("Pushing Image to GCR") {
      steps {
        script {
          sh curl https://sdk.cloud.google.com | bash && mv google-cloud-sdk /opt
          sh "PYTHONUNBUFFERED=1 gcloud builds submit -t  gcr.io/gj-playground/frontend . "
          }
        }
      }
    }
}
