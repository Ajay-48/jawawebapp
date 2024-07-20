pipeline {
    agent {
	    label 'maven-build-agent'
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "Maven3.9.8"
    }

    stages {
        stage('Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/uat']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Ajay-48/jawawebapp.git']]) 
            }
        }
        stage('Build') {
            steps {

                // Run Maven on a Unix agent.
                sh 'mvn clean install -f pom.xml'

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }
        stage('Deploy to Prod') {
            steps {
             deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://54.144.209.127:8080/')], contextPath: null, war: '**/*.war' 
            }

           
               
            
        }
             

    }
}
