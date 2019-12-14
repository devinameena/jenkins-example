pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/devinameena/jenkins-example'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@3.91.92.156:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
