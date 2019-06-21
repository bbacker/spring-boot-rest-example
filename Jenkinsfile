// first use poc-jenkins.ep.corp
pipeline {

 stages {
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/bbacker/spring-boot-rest-example'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('check out') {
         sh "echo crude way without jenkins creds"
         sh "git clone https://github.com/bbacker/spring-boot-rest-example"
   }
   stage('Build') {
      // Run the maven build
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
   }
   stage('Dockerbuild') {
        docker build -t sbdemo:${env.BUILD_ID}
   //    customImage.push()

        sh -x push_image.sh ${env.BUILD_ID}
   }
 }
}
