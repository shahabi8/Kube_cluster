pipeline {
	agent any
	stages {

		stage('Create kubernetes cluster') {
			steps {
				withAWS(credentials:'Jenkins_local') {
					sh '''
						eksctl create cluster \
						--name capstonecluster \
						--version 1.13 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto
					'''
				}
			}
		}

		
		stage('Create conf file cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'Jenkins_local') {
					sh '''
						aws2 eks --region us-east-1 update-kubeconfig --name capstonecluster
					'''
				}
			}
		}

	}
}
