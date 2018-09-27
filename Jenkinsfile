pipeline {
  agent any
  stages {
    stage('Build') {
      agent any 
      steps {
        script {
          sh 'composer install'
        }
        echo "Build success"
      }
    }
    stage('Test') {
      agent any
      steps {
        sh 'phpunit -c tests/unit/phpunit.xml tests/unit'
        echo "test success"
      }
    }
    stage('deploy or abort') {
      agent any
      steps {
          script {
              input message: 'user input required',
              ok: 'Deploy',
              abort: 'Cancel'
                    // parameters:[
                    //     choice(
                    //     choices: "deploy\nabort",
                    //     description: '',
                    //     name: 'REQUESTED_ACTION')
                    // ]
          }
      }
    }
    stage('Deploy'){
      agent any
        // when {
        //         expression { params.REQUESTED_ACTION == 'deploy' }
        //     }
        steps {
                sh 'docker-compose up'
                sh "echo success"
        }
    }
  }
}
