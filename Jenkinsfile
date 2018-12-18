pipeline {
  agent {
    label "jenkins-s2i"
  }
  environment {
    ORG               = 'jenkinsx-pw1'
    APP_NAME          = 'demo10'
    BRANCH_NAME       = "$GIT_BRANCH".replaceAll('^origin/','')
    REV               = "$GIT_COMMIT".trim().take(7)
    RELEASE_VERSION   = "$BRANCH_NAME-$BUILD_NUMBER-$REV"
    RELEASE_NAMESPACE = "$APP_NAME-$BRANCH_NAME".toLowerCase()
    IMAGE_NAME        = "$DOCKER_REGISTRY/$ORG/$APP_NAME"
  }
  stages {
    stage('Compile Build JUnit Test Push Image') {
      steps {
        container('s2i') {
          sh "s2i build . pingworks/demo-builder:2 $IMAGE_NAME:$RELEASE_VERSION"
          sh "docker push $IMAGE_NAME:$RELEASE_VERSION" 
        }
      }
    }
    stage('ACPT Deploy and Testing') {
      steps {
        container('s2i') {
          
        }
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}
