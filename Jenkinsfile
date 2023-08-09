node{
     stage('SCM Checkout'){
      git 'https://github.com/karthickshivan/my-app.git'
    }
     stage('maven-buildstage'){
      def mvnHome =  tool name: 'maven3', type: 'maven'   
      sh "${mvnHome}/bin/mvn clean package"
	  sh 'mv target/myweb*.war target/newapp.war'
    }
     stage('Build Docker Image'){
      sh 'docker build -t karthikeyan89/myweb:0.0.2 .'
    }
     stage('Docker Image Push'){
      withCredentials([string(credentialsId: 'dockerPass', variable: 'dockerPassword')]) {
      sh "docker login -u karthikeyan89 -p ${dockerPassword}"
    }
      sh 'docker push karthikeyan89/myweb:0.0.2'
    }
     stage('Docker deployment'){
      sh 'docker run -d -p 8090:8080 --name tomcattest karthikeyan89/myweb:0.0.2' 
    }
}
