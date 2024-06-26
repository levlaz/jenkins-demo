pipeline {
  agent { label 'dagger' }

  // assumes that the Dagger Cloud token
  // is in a Jenkins credential named DAGGER_CLOUD_TOKEN
  environment {
    DAGGER_CLOUD_TOKEN =  credentials('DAGGER_CLOUD_TOKEN')
  }

  // assumes a Go project
  // modify to use different function(s) as needed
  stages {
    stage("dagger") {
      steps {
        checkout ([
          changelog: false, 
          poll: false, 
          scm: scmGit(
            branches: [[name: '**']], 
            browser: github('https://github.com/levlaz/jenkins-demo'), 
            extensions: [
              cloneOption(
                honorRefspec: true, 
                noTags: true, 
                reference: '', 
                shallow: false
                ), 
                lfs(), 
                localBranch('main')
            ], 
            userRemoteConfigs: [
              [
                url: 'https://github.com/levlaz/jenkins-demo'
                ]
            ])
        ])
        sh '''
            curl -L https://dl.dagger.io/dagger/install.sh | BIN_DIR=$HOME/.local/bin sh
            /var/jenkins_home/.local/bin/dagger -m github.com/shykes/daggerverse/hello@v0.1.2 call hello --greeting=bonjour --name=daggernaut
        '''
      }
    }
  }
}
