pipeline {
     agent any
	 tools {
        maven 'maven' 
	//jdk 'jdk1.8'
    }
	 environment {
        containerName = "shraddhal/seleniumtest2"
        container_version = "1.0.0.${BUILD_ID}"
        dockerTag = "${containerName}:${container_version}"
		     
    }
    stages { 	
	    stage('Clone repository') {
			   steps {	       
				 git 'https://github.com/shraddhaL/selenium_repo2.git' }
        
			   }
	    
	/*     stage('copy Artifacts') {
            steps {
                script {
			copyArtifacts filter: 'propsfile', fingerprintArtifacts: true, projectName: 'deploy_to_container', selector: workspace()
                }
	    }
        }  */
	    
	   stage('Build Jar') {
	    
		steps {
		   	//////sh'docker stop $(docker ps -q) || docker rm $(docker ps -a -q) || docker rmi $(docker images -q -f dangling=true)'
        		//bat 'docker system prune --all --volumes --force'
			
			
			//sh 'var=$(cat propsfile)|echo $var'
			//sh ''//temp=cat propsfile | mvn -Dxyz="$TEMP"
			sh 'mvn clean package -DskipTests'
		    //   sh 'mvn clean package -DskipTests -Duuid=$var'
        }
        }
	   
	 
	    
	    stage('compose') {
            steps {
                script {
			//sh 'docker run -d -p 4444:4444 --memory="1.5g" --memory-swap="2g" -v /dev/shm:/dev/shm selenium/standalone-chrome'
			sh 'docker-compose up -d --scale chrome=3'
			
                }
	    }
        }
	 
	     stage('archive Artifacts') {
            steps {
                script {
			archiveArtifacts artifacts: 'docker-compose.yml', followSymlinks: false
			}
	    }
        }  
	    



	 stage('test') {
            steps {
		    script {
		    sh 'cat propsfile'
			//--> //sh 'mvn -Dtest="SearchTest.java,SearchTest2.java" test'
			sh 'mvn -Dtest="SearchTest.java" test'
                }
	    }
	 }
	    
	
}
}
