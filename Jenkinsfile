
node {

   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/denisdbell/spring-petclinic.git'
    
   }
   stage('Build Maven Image') {

	sh " echo Giving Jenkins Right Permissions to Use Docker "
        sh "sudo chown root:jenkins /run/docker.sock"
        sh " echo Current User is : $USER "
	docker.build("maven-build")
   }
   
   stage('Run Maven Container') {
       
        //Remove maven-build-container if it exisits
        sh " docker rm -f maven-build-container"
        
        //Run maven image
        sh " docker run --rm --name maven-build-container maven-build"
   }
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exisits
        sh " docker rm -f java-deploy-container"
       
        sh " docker run --name java-deploy-container --volumes-from maven-build-container -d -p 8082:8082 denisdbell/petclinic-deploy"
   }

}
