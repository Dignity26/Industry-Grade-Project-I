pipeline {
    agent none
        tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }
    stages {
        stage('SCM') {
            agent {
                label 'node1'
            }
            steps {
                        // Your build steps for Node 1
                sh 'rm -rf /var/lib/jenkins/workspace/Sample-Project-1/'
                git branch: 'main', url: 'https://github.com/Dignity26/Industry-Grade-Project-I.git'
            }
        }
        stage('build') {
            agent {
                label 'node1'
            }
            steps {
                        // Your build steps for Node 2
                sh "mvn package"
            }
        }
        stage('Build and Push Docker image') {
            agent {
                label 'node1'
            }
            steps {
                script{
                   sh 'ansible-playbook build_and_push_docker.yml'
				}
                
            }
        }
        stage('Deploy on Kubernetes') {
            agent {
                label 'node2'
            }
            steps {
                //sh 'kubectl delete -f deployment.yml'
                sh 'rm -rf /var/lib/jenkins/workspace/Sample-Project-1'
                git branch: 'main', url: 'https://github.com/Dignity26/Industry-Grade-Project-I.git'
                sh 'kubectl  apply -f deployment.yml'
				sh 'kubectl  apply -f service.yml'
				
                   
				               
            }
        }
            
    }
    
}
