pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-cred-sudheer')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t sudheer1994/test:1.0.0 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'
			}
		}


		stage('Push') {

			steps {
				sh 'docker push sudheer1994/test:1.0.0'
			}
		}


		stage('Deploy to K8s')
		{
			steps{
				sshagent(['k8s-jenkins'])
				{
					sh 'scp -r -o StrictHostKeyChecking=no node-deployment.yaml username@18.118.101.96:/path'
					
					script{
						try{
							sh 'ssh username@18.118.101.96 kubectl apply -f ./deployment.yaml --kubeconfig=/path/kube.yaml'
       sh 'ssh username@18.118.101.96 kubectl apply -f ./service.yaml --kubeconfig=/path/kube.yaml'
       sh 'ssh username@18.118.101.96 kubectl apply -f ./k8s-ingress.yaml --kubeconfig=/path/kube.yaml'

							}catch(error)
							{

							}
					}
				}
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
