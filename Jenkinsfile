pipeline {
  agent any

  tools {
      maven 'M2_HOME'
      terraform 'terraform-11'
        }
environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        }


  stages {
     stage('checkout'){
       steps {
         echo 'checkout the code from GitRepo'
          git 'https://github.com/prafullashilimkar/star-agile-banking-finance.git'
                    }
            }
   

     stage('Build the  Application'){
               steps {
                   echo "Cleaning.... Compiling......Testing.........Packaging"
                   sh 'mvn clean package'
                    }
                 }
     stage('publish Reports'){
               steps {
               publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Bankingproject/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])    
                    }
            }

//      stage('Docker Image Creation'){
 //              steps {
  //                    sh 'docker build -t prafullla/bankingapp:latest  .'
 //                     }
 //                  }


//      stage('Push Image to DockerHub'){
//               steps {
//                   withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
//        	   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
 //                  sh 'docker push prafullla/bankingapp:latest'

//	            }
 //                }
//            }
     stage ('Configure Test-server with Terraform, Ansible and then Deploying'){
            steps {
                dir('test-server')  { 
                sh 'sudo chmod 600 jenkinskey1.pem'
                sh 'terraform init'
                sh 'terraform validate'
                sh 'terraform apply --auto-approve'
                }                
                }
                }
      }
  }
