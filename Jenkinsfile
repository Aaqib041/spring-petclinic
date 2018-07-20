
node {

   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/denisdbell/spring-petclinic.git'
    
   }
   stage('Build Maven Image') {

	sh " echo Building Docker File "
       // sh "sudo chown root:jenkins /run/docker.sock"
        sh " echo Current User is : $USER "
	//docker.build("maven-build")
	sh 'docker build -t "akeeb/petclinic" .'
   }
   
   stage('Run Maven Container') {
       
        //Remove maven-build-container if it exisits
       // sh " docker rm -f maven-build-container"
        
        //Run maven image
        sh " docker run  --name maven-build-container akeeb/petclinic"
   }
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exisits
       //sh " docker rm -f java-deploy-container"
       
        sh " docker run --name java-deploy-container --volumes-from maven-build-container -d -p 8092:8082 denisdbell/petclinic-deploy"
   }

}
