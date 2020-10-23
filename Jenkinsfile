node {
    def bluesite = 'mreddy7/capstoneblue'
    def greensite = 'mreddy7/capstonegreen'
    stage('Setup and check Env') {
      echo 'Git Checkout and check environment'
      sh 'git --version'
      sh 'docker -v'
      checkout scm
    }
    stage("Linting HTML") {
      echo 'Linting'
      sh '/usr/bin/hlint blue/Dockerfile'            
    }
    stage('Docker Blue image') {
	    echo 'Building Docker Blue image'
      withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerhubpwd')]) {
	     	sh 'docker login -u mreddy7 -p ${env.dockerHubPassword}'
	     	sh 'sudo docker build -t ${bluesite} blue/.'
	     	sh 'sudo docker tag ${bluesite} ${bluesite}'
	     	sh "sudo docker push ${bluesite}"
      }
    }
    stage('Docker Green image') {
	    echo 'Building Docker image green'
      withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerhubpwd')]) {
	     	sh 'docker login -u mreddy7 -p ${env.dockerHubPassword}'
	     	sh "sudo docker build -t ${greensite} blue/."
	     	sh "sudo docker tag ${greensite} ${greensite}"
	     	sh "sudo docker push ${greensite}"
      }
    }
    stage('Deploy') {
      echo 'Deploying to AWS EKS...'
      dir ('./') {
      withAWS(credentials: 'ecr-credentials-aws', region: 'us-west-2') {
          sh "aws eks --region us-west-2 update-kubeconfig --name capstone-devops"
          sh "kubectl apply -f blue/blue-controller.yaml"
          sh "kubectl apply -f green/green-controller.yaml"
          sh "kubectl apply -f ./website-service.yaml"
          sh "kubectl get nodes"
          sh "kubectl get deployment"
          sh "kubectl get pods"
        }
      }
    }
}
