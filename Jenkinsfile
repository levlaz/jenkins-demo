pipeline {
  agent { label 'dagger' }

  // assumes that the Dagger Cloud token
  // is in a Jenkins credential named DAGGER_CLOUD_TOKEN
  environment {
    DAGGER_CLOUD_TOKEN =  credentials('DAGGER_CLOUD_TOKEN')
  }

  stages {
    stage("dagger") {
      steps {
        sh 'git branch'
        sh 'echo new branch'
        sh '''
            curl -L https://dl.dagger.io/dagger/install.sh | BIN_DIR=$HOME/.local/bin sh
            /var/jenkins_home/.local/bin/dagger -m github.com/shykes/daggerverse/hello@v0.1.2 call hello --greeting=bonjour --name=daggernaut
        '''
      }
    }
  }
}
