// first use poc-jenkins.ep.corp
pipeline {
agent { label 'master'}

 stages {
   stage('check out') {
    steps {
         sh "echo crude way without jenkins creds"
         sh "git clone https://github.com/bbacker/spring-boot-rest-example"
    }
   }
   stage('Build') {
    steps {
      // Run the maven build
         sh "cd spring-boot-rest-example; ~/tools/maven/bin/mvn -Dmaven.test.failure.ignore clean package"
    }
   }
   stage('Dockerbuild') {
    steps {
        sh "cd spring-boot-rest-example; docker build -t sbdemo:${env.BUILD_ID}"
        sh " push_image.sh ${env.BUILD_ID}"
    }
   }
 }
}
