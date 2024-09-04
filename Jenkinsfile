pipeline {
 
 agent any
     
    stages {
        stage('Getting Project from Git') {
            steps {
                echo 'Project is downloading...'
                git branch:'master', url:'https://github.com/03sarath/jenkins-mlflow-docker.git'
  
                 }
             }
          stage('Building docker container') {
            steps {
                  bat 'docker build -t heartdisease-model .'
                  bat 'docker run -d --name model heartdisease-model'
               }
           }
            stage('Preprocessing stage') {
            steps {
                   bat 'docker container exec model python3 preprocessing.py'
               }
           }
           stage('Training stage') {
            steps {
                    bat 'docker container exec model python3 train.py'
                }
        }
        stage('Test stage') {
              steps {
                    bat 'docker container exec model python3 train.py'
                    bat 'docker container exec model python3 test.py'
                    bat 'docker rm -f model'
                  }
               }
    }
}