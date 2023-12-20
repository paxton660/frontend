pipeline {
  agent {
    kubernetes {
      label 'sample-app'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  containers:
  - name: gcloud-kubectl-docker
    image: gcr.io/turing-goods-403608/gcloud-kubectl-docker
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage('Build and push image with Container Builder') {
      steps {
        container('gcloud-kubectl-docker') {
          sh "gcloud auth activate-service-account --key-file=turing-goods-403608-f870fe0f69e1.json"
          sh "gcloud config set project turing-goods-403608"
          sh "PYTHONUNBUFFERED=1 gcloud builds submit -t gcr.io/turing-goods-403608/frontend ."
        }
      }
   }
    stage('deployment'){
      steps{
        container('gcloud-kubectl-docker'){
          sh"gcloud container clusters get-credentials cluster-3 --zone us-central1-c --project turing-goods-403608 "
          sh"kubectl apply -f frontendservice.yaml"
}
}

      }
    }
  }
