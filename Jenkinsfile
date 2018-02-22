imageName = 'area51/java'

steps = [ 'jdk', 'jre', 'serverjre' ]
properties( [
  buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '7', numToKeepStr: '10')),
  disableConcurrentBuilds(),
  disableResume(),
  pipelineTriggers([cron('H H * * *')])
])

node( 'Dev_AMD64_Amsterdam' ) {
  stage( 'Checkout' ) {
    checkout scm
  }

  stage( 'Prepare Build' ) {
    sh 'docker pull area51/alpine:latest'
  }

  steps.each {
    step -> stage( 'Build Java8 ' + step ) {
      sh 'docker build -t ' + imageName + ':' + step + '-8 ' + step
    }
  }

  steps.each {
    step -> stage( 'Publish Java8 ' + step ) {
      sh 'docker push ' + imageName + ':' + step + '-8'
    }
  }

  stage( 'Publish Image' ) {
    sh 'docker push ' + imageName
  }
}
