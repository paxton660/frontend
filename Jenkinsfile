pipeline {
  environment {
    PROJECT = "gj-playground"
    CLUSTER = "gke-cluster-public"
    CLUSTER_ZONE = "asia-southeast1-a"
    IMAGE_TAG = "gcr.io/gj-playground/frontend"
  }
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      yaml """"
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  containers:
  - name: java
    image: openjdk:8-slim
    command:
    - cat
    tty: true
  - name: gcloud
    image: gcr.io/google.com/cloudsdktool/cloud-sdk:latest
    command:
    - cat
    tty: true
  
  ""
}
  }
  stages {
    stage('Test') {
      steps {
        container('java') {
          sh ""
            echo “******** currently executing Test stage ********”
          ""
        }
      }
    }
    stage('Build and push image with Container Builder') {
      steps {
        container('gcloud') {
          sh "gcloud auth list"
          sh "PYTHONUNBUFFERED=1 gcloud builds submit -t  gcr.io/gj-playground/frontend . "
        }
      }
    }
}

}
