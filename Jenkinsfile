pipeline {
  
  stages {
    stage('Bake') {
      steps {
        container('gcloud') {
            sh '''
            sh "gcloud auth list"
            sh "PYTHONUNBUFFERED=1 gcloud builds submit -t  gcr.io/gj-playground/adservice . "
            '''
        }
      }
      
      }
    }
}
