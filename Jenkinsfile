// first use poc-jenkins.ep.corp
pipeline {

 stages {
   stage('check out') {
         sh "echo crude way without jenkins creds"
         sh "git clone https://github.com/bbacker/spring-boot-rest-example"
   }
   stage('Build') {
      // Run the maven build
         sh "cd spring-boot-rest-example; ~/tools/maven/bin/mvn -Dmaven.test.failure.ignore clean package"
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
   }
   stage('Dockerbuild') {
        sh "cd spring-boot-rest-example; docker build -t sbdemo:${env.BUILD_ID}"
        sh " push_image.sh ${env.BUILD_ID}"
   }
 }
}
