pipeline {
    agent {
        node {
            label 'Jenkins-slave-node'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
        scannerHome = tool 'sonar-scanner-meportal'
    }
    stages {
        stage("Build") {
            steps {
                echo "Build started"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "Build completed"
            }
        }
          stage("test stage"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test Completed ----------"
            }
        }
      
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar-server-meportal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
