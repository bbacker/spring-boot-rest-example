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
        sh "cd spring-boot-rest-example; docker build -t sbdemo:${BUILD_ID} ."
//        sh " push_image.sh ${BUILD_ID}"

/* TODO: change to form using jenkins creds
  https://wiki.jenkins.io/display/JENKINS/Amazon+ECR

  stage 'Docker push'
  docker.withRegistry('https://1234567890.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:demo-ecr-credentials') {
    docker.image('demo').push('latest')
  }
*/

        sh '''
        aws ecr get-login --no-include-email --region us-west-2 > ./login
        . ./login
        docker tag sbdemo:${BUILD_ID} 589011911289.dkr.ecr.us-west-2.amazonaws.com/bbtest:${BUILD_ID}
        docker push "589011911289.dkr.ecr.us-west-2.amazonaws.com/bbtest:${BUILD_ID}"
        '''
    }
   }
 }
}
