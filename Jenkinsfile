pipeline {
    agent none
    stages {
        stage('Build') {
            agent {label 'slave2'}
            steps {
                git branch: 'main', url: 'https://github.com/rajath177/java-project.git'
                sh '''
                    cd /home/ec2-user/java/workspace/pipeline-job2
                    mvn clean install
                '''    
            }
        }
        stage('Deploy') {
            agent {label 'slave2'}
            steps {
                sh 'scp /home/ec2-user/java/workspace/pipeline-job2/target/works-with-heroku-1.0.war ec2-user@172.31.38.118:/home/ec2-user/tomcat/webapps'
                sh 'echo "war file deployed to tomcat" >> log-deploy-file'
            }
        }
        stage('Testing') {
            agent {label 'slave2'}
            steps {
                sh '''
                    echo "test cases are tested" >> log-test-file
                '''
            }            
        }
    }
}
