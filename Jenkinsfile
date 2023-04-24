pipeline {
    agent any
    stages {
        stage('code from scm') {
            steps {
                git 'https://github.com/poorna162/Poorna.git'
            }
        }
        stage('building the code') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('unit test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('code quality') {
            steps {
                sh 'mvn checkstyle:checkstyle'
                recordIssues(tools: [checkStyle(pattern: '**/checkstyle-result.xml')])
            }
        }
        stage('code quality sonar') {
            steps {
               sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=sonar_project \
  -Dsonar.projectName='sonar_project' \
  -Dsonar.host.url=http://182.18.184.72:9000 \
  -Dsonar.token=sqp_3a15594e8760538bb4c8e37807f5e6ed53a230aa"
            }
        }
        
    }
    
    
}
