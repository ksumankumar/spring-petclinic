pipeline {
    agent { label 'JDK-11'}
    parameters {
        choice(name: 'BUILD', choices: ['release-para', 'main'], description: 'Branch to build')
        string(name: 'GOAL', defaultValue: 'package', description: 'maven goal')
    }
    triggers{
        pollSCM('* * * * *')
    }
    stages {
        stage ('source code  from git remote repository') {
            steps {
                mail subject: 'Build Started',
                     body: 'Build Started',
                     to: 'ksumandora32@gmail.com'
                git url: "https://github.com/ksumankumar/spring-petclinic.git",
                branch: "${params.BUILD}"
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn ${params.GOAL}" 
            }
        }
    post {
        always {
            echo 'job completed'
            mail subject: 'Build Completed',
                 body: 'Build Completed',
                 to: 'ksumandora32@gmail.com'
        }
        failure {
            mail subject: 'Build Failed',
                 body: 'Build Failed',
                 to: 'ksumandora32@gmail.com'
        }
        success {
            archiveArtifacts artifacts: 'target/*.jar',
            junit '**/surefire-reports/*.xml'
        }         
    }    
        
    }
}    
         
           
         
        
    

