pipeline {
    agent any
triggers {
  pollSCM '* * * * * '
}
    stages {
        stage('Git') {
            steps {
                git branch: 'feat01', changelog: false, url: 'https://github.com/Ajayaws773/mavenrepo.git'
            }
        }
		
		stage('build') {
            steps {
                sh 'mvn package'
            }
        }
		
		stage('Scanning') {
            steps {
                withSonarQubeEnv('sonarqube') {
                sh 'mvn sonar:sonar' 
}
            }
        }
		
		stage('artifact') {
            steps {
                sh 'mvn deploy'
            }
        }
		
		stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.109.124.135:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
