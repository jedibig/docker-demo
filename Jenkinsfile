pipeline {
  agent any
  stages {
    stage('Github') {
      agent any
      steps {
        git 'https://github.com/jedibig/docker-demo.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package'
        archiveArtifacts(artifacts: '**/target/surefire-reports/TEST-*.xml', allowEmptyArchive: true, onlyIfSuccessful: true)
      }
    }

    stage('Deploy') {
      agent any
      environment {
        dockertag = '3'
        password = ''
      }
      steps {
        sh 'sh \'mvn deploy -Ddocker-tag={dockertag} -Dpassword=${password}\''
      }
    }

  }
  environment {
    dockertag = '1'
  }
}
