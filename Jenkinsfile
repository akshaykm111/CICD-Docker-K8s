pipeline {
	agent any

	stages {
	  stage('Fetch Code') {
	    steps {
	      git branch: 'FlightBook', url: 'https://github.com/akshaykm111/CICD-Docker-K8s.git'
	    }
	  }
	  stage('Build Docker') {
	    steps {
	      script {
	         sh '''
				docker build -t kubeakshay111/flightbook:V${BUILD_NUMBER} .
				'''
		  }
		}
	  }
	}
}	