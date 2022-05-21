pipeline {
	agent any
		stages{
			stage('saving nginx image on staging server') {
				sh '''SSH_ARGS="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
				sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo docker save nginx_test > /home/prashanth/nginxprod.tar  "'''
				
		}

			stage('getting image from staging to production'){
				sh '''SSH_ARGS="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
				sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.227 "sudo scp -q /home/prashanth/nginxprod.tar prashanth@172.29.87.69:/home/prashanth/ "'''

		}

			stage('Loging image on production server'){
				sh '''SSH_ARGS="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
				sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.69 " sudo docker load < /home/prashanth/nginxprod.tar"'''

		}

		stage('Creating container on production server'){
			   sh '''SSH_ARGS="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
			   sshpass -p \'9246\' ssh ${SSH_ARGS}  prashanth@172.29.87.69 "sudo docker stop nginx_web && sleep 5 && sudo docker rm nginx_web && sleep 5 &&sudo docker run -d --name nginx_web --privileged=true -p 900:80 nginx_test:latest  /usr/sbin/init && sleep 5 && sudo docker exec nginx_web systemctl start nginx"'''

		}



	}

		
		

}
