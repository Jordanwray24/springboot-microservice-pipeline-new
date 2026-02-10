pipeline {
  agent any

  environment {
    AWS_REGION = "us-east-1"
    AWS_ACCOUNT_ID = "478860598824"
    ECR_REPO = "springboot-microservice"
    ECR_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${ECR_REPO}"
    IMAGE_TAG = "${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build & Test (Maven)') {
      steps { sh 'mvn -B clean test package' }
      post {
        always {
          archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
          junit 'target/surefire-reports/*.xml'
        }
      }
    }

    stage('Docker Build') {
      steps {
        sh """
          docker build -t ${ECR_URI}:${IMAGE_TAG} .
          docker tag ${ECR_URI}:${IMAGE_TAG} ${ECR_URI}:latest
        """
      }
    }

    stage('ECR Login & Push') {
      steps {
        sh """
          aws ecr describe-repositories --repository-names ${ECR_REPO} --region ${AWS_REGION} >/dev/null 2>&1 || \
          aws ecr create-repository --repository-name ${ECR_REPO} --region ${AWS_REGION}

          aws ecr get-login-password --region ${AWS_REGION} | \
          docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com

          docker push ${ECR_URI}:${IMAGE_TAG}
          docker push ${ECR_URI}:latest
        """
      }
    }

    stage('Deploy (Ansible)') {
      steps {
        sh """
          ansible-playbook -i ansible/inventory.ini ansible/playbooks/deploy_app.yml \
            --extra-vars "aws_region=${AWS_REGION} aws_account_id=${AWS_ACCOUNT_ID} ecr_uri=${ECR_URI} image_tag=${IMAGE_TAG}"
        """
      }
    }
  }
}
