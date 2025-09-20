// pipeline {
//     agent any
    
//     parameters {
//         choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select the Terraform action to perform')
//     }

//     stages {
//         stage('Cloning github repo') {
//             steps {
//                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Rajvardhan-128/Infrastructure_management_project.git']])
//             }
//         }
    
//          stage ("terraform init") {
//              steps {
//                  sh ("terraform init -reconfigure") 
//              }
//          }
        
//         stage ("terraform Plan") {
//             steps {
//                 sh ("terraform plan") 
//             }
//         }

//         stage ("Action") {
//             steps {
//                 echo "Terraform action is --> ${action}"
//                 sh ('terraform ${action} --auto-approve') 
//            }
//         }
//     }
// }


pipeline {
    agent any
    
    parameters {
        choice(name: 'action', choices: ['plan', 'apply', 'destroy'], description: 'Select the Terraform action to perform')
    }

    stages {
        stage('Cloning github repo') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Rajvardhan-128/Terraform_Infrastructure_management_project.git']])
            }
        }
    
        stage("Terraform Init") {
            steps {
                sh "terraform init -reconfigure"
            }
        }
        
       

        stage("Action") {
            steps {
                script {
                    echo "Terraform action is --> ${params.action}"
                    sh "terraform ${params.action} --auto-approve"
                }
            }
        }
    }
}
