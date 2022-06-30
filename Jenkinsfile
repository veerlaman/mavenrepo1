pipeline {
    agent any
triggers {
  pollSCM '* * * * *'
}
    stages {
        stage('SCM') {
            steps {
                git branch: 'feat01', changelog: false, poll: false, url: 'https://github.com/Ajayaws773/mavenrepo.git'
            }
        }
		 stage('maven build') {
            steps {
                sh 'mvn package'
            }
        }
		stage('Sonar') {
            steps {
			withSonarQubeEnv('sonarqube') {
            sh 'mvn sonar:sonar'
            }
                
            }
        }
		stage('Nexus') {
            steps {
			    sh 'mvn deploy'
            }
        }
		         
		stage('tomcat') {
            steps {
			    deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.109.124.135:8080/')], contextPath: 'studentapp', war: '**/*.war'
            }
        }
    }
}


