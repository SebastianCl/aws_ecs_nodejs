@Library('github.com/releaseworks/jenkinslib') _
pipeline {
    agent any
    parameters {
    gitParameter branchFilter: 'origin/(.*)', defaultValue: 'dev', name: 'BRANCH', type: 'PT_BRANCH'
    }
    environment { 
        //---------------------------REPO---------------------------
        GIT_URL_PROYECT="${GITHUB_URL}/locoalien/aws_ecs_nodejs"
        GIT_BRANCH_DEFINED="dev"
        GIT_CREDENTIALS_ID='githublocoalien'
        CONTAINER_NAME="aws_ecs_nodejs"
        CONTAINER_NAME_COMPOSE="aws_ecs_nodejs"
        //---------------------------AWS CONFIG---------------------------
        ACCOUNT_ID = "512938095486"
        REGION = "us-west-2"
        REPOSITORY_NAME_DOCKER = "my-first-ecr-repo"
        AWS_ACCESS_KEY_ID     = "${ACCESS_KEY_AWS_NEWINNTECH}"
        AWS_SECRET_ACCESS_KEY = "${SECRET_KEY_AWS_NEWINNTECH}" // Referencia: https://coralogix.com/log-analytics-blog/ci-cd-tutorial-how-to-deploy-an-aws-jenkins-pipeline/

    }
    stages{
        stage("Obteniendo codigo fuentes"){
            steps{
                echo "Clonando el BRANCH: ${params.BRANCH}"                
                git branch: "${params.BRANCH}", credentialsId:GIT_CREDENTIALS_ID, url:GIT_URL_PROYECT
                echo "El numero de compilacion es: ${env.BUILD_NUMBER}"             
            }
        }

        stage("AWS ECS (Terraform)"){
            steps{
                withEnv(["AWS_ACCESS_KEY_ID=${ACCESS_KEY_AWS_NEWINNTECH}", "AWS_SECRET_ACCESS_KEY=${SECRET_KEY_AWS_NEWINNTECH}", "AWS_DEFAULT_REGION=${REGION}"]) {
                    //Terraform("destroy -auto-approve")
                    //Terraform("init")
                    Terraform("destroy -auto-approve")
                    //Terraform("plan")
                    //Terraform("import aws_key_pair.deployer aws_rsa")
                    //Terraform("apply -auto-approve ")
                    //Terraform("validate")  
                } 
                script{
                    //sh "aws configure set region ${REGION}"
                    //CLAVE = sh([ script: "aws ecr get-login-password --region us-west-2", returnStdout: true ]).trim()
                    //sh "echo ${CLAVE}"
                    //sh "docker login --username AWS --password ${CLAVE} 512938095486.dkr.ecr.us-west-2.amazonaws.com"
                    //En caso de problemas con el Login, se debe instalar en el servidor lo siguiente: sudo apt install gnupg2 pass
                    //sh "aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com"
                    //sh "docker build -t ${REPOSITORY_NAME_DOCKER} ."
                    //sh "docker tag ${REPOSITORY_NAME_DOCKER}:latest ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${REPOSITORY_NAME_DOCKER}:latest"
                    //sh "docker push ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${REPOSITORY_NAME_DOCKER}:latest"
                }  
                      
            }
        }
    }
}
 
