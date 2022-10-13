pipeline {
    agent { label 'JDK-11'}
    parameters {
        choice(name: 'BUILD', choices: ['release-para', 'main'], description: 'Branch to build')
        string(name: 'GOAL', defaultValue: 'package', description: 'maven goal')
    }
    triggers {
       pollSCM('* * * * *')
    }
    stages {
        stage ('source code  from git remote repository') {
            steps {
                mail subject: "Build Started for Jenkins JOB $env.JOB_NAME",
                     body: "Build Started for Jenkins JOB $env.JOB_NAME",
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
		stage("archive artifact") {
            steps { 
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
	}		
    post {
        always {
            echo 'job completed'
            mail subject: "Build Completed for Jenkins JOB $env.JOB_NAME",
                 body: "Build Completed for Jenkins JOB $env.JOB_NAME \n Click Here $env.JOB_URL",
                 to: 'ksumandora32@gmail.com'
        }
        failure {
            mail subject: "Build Failed for Jenkins JOB $env.JOB_NAME with Build ID $env.BUILD_ID",
                 body: "Build Failed for Jenkins JOB $env.JOB_NAME",
                 to: 'ksumandora32@gmail.com'
        }
        success {
            junit '**/surefire-reports/*.xml'
        }
    } 
}             
   
         
           
         
        
    

