pipeline {
    agent any
 
    environment {
        APP_NAME_apigateway = 'apigateway'
        APP_NAME_identity = 'identity'
        APP_NAME_textile = 'textile'
        APP_NAME_production = 'production'
        APP_NAME_ie = 'ie'
        APP_NAME_hr_payroll = 'clickerp/hr-payroll'
        APP_NAME_store = 'clickerp/store'
    }

    stages {
        
        stage('Clear') {
            steps {
                deleteDir()
            }
        }
        
        stage('checkout scm') {
            steps {
                withCredentials([gitUsernamePassword(credentialsId: 'github_uk', gitToolName: 'Default')]) {
                    checkout scmGit(
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'https://github.com/ClickERPDevlopment/ClickErp_Deployment.git']])
                }
            }
        }
        
        stage('Updating apigateway kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/apigateway/deployment.yaml
                        sed -i 's/${APP_NAME_apigateway}.*/${APP_NAME_apigateway}:${IMAGE_TAG}/g' k8s/apigateway/deployment.yaml
                        cat k8s/apigateway/deployment.yaml 
                    """
                }
            }
        }
        
        stage('Updating identity kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/identity/deployment.yaml
                        sed -i 's/${APP_NAME_identity}.*/${APP_NAME_identity}:${IMAGE_TAG}/g' k8s/identity/deployment.yaml
                        cat k8s/identity/deployment.yaml 
                    """
                }
            }
        }
        
        stage('Updating textile kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/textile/deployment.yaml
                        sed -i 's/${APP_NAME_textile}.*/${APP_NAME_textile}:${IMAGE_TAG}/g' k8s/textile/deployment.yaml
                        cat k8s/textile/deployment.yaml 
                    """
                }
            }
        }
        
        // stage('Updating ie kubernetes deploymnet file') {
        //     steps{
        //         script{
        //             sh """
        //                 cat k8s/ie/deployment.yaml
        //                 sed -i 's/${APP_NAME_ie}.*/${APP_NAME_ie}:${IMAGE_TAG}/g' k8s/ie/deployment.yaml
        //                 cat k8s/ie/deployment.yaml 
        //             """
        //         }
        //     }
        // }
        
        stage('Updating production kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/production/deployment.yaml
                        sed -i 's/${APP_NAME_production}.*/${APP_NAME_production}:${IMAGE_TAG}/g' k8s/production/deployment.yaml
                        cat k8s/production/deployment.yaml 
                    """
                }
            }
        }
        
        stage('Updating hr-payroll kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/hr-payroll/deployment.yaml
                        sed -i 's|${APP_NAME_hr_payroll}:[0-9]\+|${APP_NAME_hr_payroll}:${IMAGE_TAG}|g' k8s/hr-payroll/deployment.yaml
                        cat k8s/hr-payroll/deployment.yaml 
                    """
                }
            }
        }
        
        stage('Updating store kubernetes deploymnet file') {
            steps{
                script{
                    sh """
                        cat k8s/store/deployment.yaml
                        sed -i 's|${APP_NAME_store}:[0-9]\+|${APP_NAME_store}:${IMAGE_TAG}|g' k8s/store/deployment.yaml
                        cat k8s/store/deployment.yaml 
                    """
                }
            }
        }
        
        stage('Push the changed deployment file to Git') {
            steps{
                script{
                    sh """
                        git config --global user.name "MamunAG"
                        git config --global user.email "mamun166036@yahoo.com"
                        git add .
                        git commit -m "updated the deployment file"
                    """
                    
                    withCredentials([gitUsernamePassword(credentialsId: 'github_uk', gitToolName: 'Default')]) {
                        sh "git push origin HEAD:main"
                    }
                    
                }
            }
        }
    }
}