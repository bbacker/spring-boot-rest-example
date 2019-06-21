// first use poc-jenkins.ep.corp
pipeline {
agent { label 'master'}

 stages {
   stage('check out') {
    steps {
         sh "echo crude way without jenkins creds"
         sh '''
            if [ -e spring-boot-rest-example ] ;
            then
                git pull spring-boot-rest-example
            else
                git clone https://github.com/bbacker/spring-boot-rest-example
            fi
            '''
    }
   }
   stage('Build') {
    steps {
         sh "cd spring-boot-rest-example; ~/tools/maven/bin/mvn -Dmaven.test.failure.ignore clean package"
    }
   }
   stage('Dockerbuild') {
    steps {
        sh "cd spring-boot-rest-example; docker build -t sbdemo:${env.BUILD_ID} ."
        sh " push_image.sh ${env.BUILD_ID}"
    }
   }
 }
}
