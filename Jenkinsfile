pipeline {
	agent any

		stages{
			stage('saving nginx image on staging server'){
				steps{
					sh '''SSH_ARGS="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
				    sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker save nginx_test > /home/prashanth/nginxprod.tar  "'''

				}

			}




		}

}
