pipeline {

    agent any
	
    stages {
        stage('Git Clone') { 
            steps {
	      sh 'ssh -i /var/jenkins_home/chaves/chave_aws.pem admin@54.163.61.214 git clone -b producao https://github.com/GuilhermeAuras/yamls_scripts_k8s.git | if [ $? -eq 0 ]; then echo "sucesso git clone -b producao" >> /var/jenkins_home/monitor/monitor_pipeline.log; else echo "falhou git clone - producao"; fi'
            }
        }
        stage('Deploy k8s Nginx') { 
            steps {
              sh 'ssh -i /var/jenkins_home/chaves/chave_aws.pem admin@54.163.61.214 kubectl apply -f /home/admin/yamls_scripts_k8s/site_projeto_nginx/ | if [ $? -eq 0 ]; then echo "sucesso kubectl apply" >> /var/jenkins_home/monitor/monitor_pipeline.log; else echo "falhou kubectl apply"; fi'
            }
        }
        stage('Delete Deploys Nginx Directory') { 
            steps {
	      sh 'ssh -i /var/jenkins_home/chaves/chave_aws.pem admin@54.163.61.214 rm -r /home/admin/yamls_scripts_k8s/ | if [ $? -eq 0 ]; then echo "sucesso em deletar o diretorio do deploy" >> /var/jenkins_home/monitor/monitor_pipeline.log; else echo "falhou em apagar o diretorio do deploy"; fi'	    
            }
        }    		
        stage('Checkout Deploy k8s Nginx') { 
            steps {
              sh 'ssh -i /var/jenkins_home/chaves/chave_aws.pem admin@54.163.61.214 kubectl get all | grep nginx | if [ $? -eq 0 ]; then echo "sucesso kubectl get all | grep nginx" >> /var/jenkins_home/monitor/monitor_pipeline.log; else echo "falhou kubectl get all | grep nginx"; fi' 
            }
        }
        stage('Notification') { 
            steps {
              sh 'cat /var/jenkins_home/monitor/monitor_pipeline.log && rm /var/jenkins_home/monitor/monitor_pipeline.log'		    
            }
        }  
 
    }
}
