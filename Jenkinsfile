node {
    stage('Setup and check Env') {
      echo 'Git Checkout and check environment'
    }
    stage("Linting HTML") {
      echo 'Linting'
      sh 'tidy -q -e index.html'              
    }
    stage('Docker Blue image') {
	    echo 'Building Docker Blue image'
    }
    stage('Docker Green image') {
	    echo 'Building Docker image green'
    }
    stage('Deploy') {
      echo 'Deploying to AWS EKS...'
    }
}
