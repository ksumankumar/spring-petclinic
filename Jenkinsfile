pipeline {
    agent { label 'JDK-11'}
    parameters {
        choice(name: 'BUILD', choices: ['release-para', 'main'], description: 'Branch to build')
        string(name: 'GOAL', defaultValue: 'package', description: 'maven goal')
    }
    triggers{
        pollscm("* * * * *")
    }
    stages {
        stage ('source code  from git remote repository') {
            steps {
                git url: "https://github.com/ksumankumar/spring-petclinic.git",
                 branch: "${params.BUILD}"
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn ${params.GOAL}" 
            }
        }
        stage("archive artifact") {
            steps { 
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
        stage("junit Reports") {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}    
         
           
         
        
    

