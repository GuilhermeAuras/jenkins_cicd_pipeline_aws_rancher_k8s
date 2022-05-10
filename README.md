* Configure o container do Jenkins com a chave .pem da Aws:
<br>mkdir -p /var/jenkins_home/chaves/
<br>cd /var/jenkins_home/chaves/
<br>touch sua_chave.pem #cole o conteudo da chave .pem
<br>chmod 400 sua_chave.pem

* Configure o Jenkis para receber o arquivo Jenkinsfile na pipeline.
