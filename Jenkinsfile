imageName = 'area51/java'

images = [ 'jdk', 'jre', 'serverjre' ]

properties( [
  buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '7', numToKeepStr: '10')),
  disableConcurrentBuilds(),
  disableResume(),
  pipelineTriggers([
    upstream('/peter-mount/alpine/master')
  ])
])

node( 'Dev_AMD64_Amsterdam' ) {
  stage( 'Checkout' ) {
    checkout scm
  }

  stage( 'Prepare Build' ) {
    sh 'docker pull area51/alpine:latest'
  }

  images.each {
    image -> stage( 'Build Java8 ' + image ) {
      sh 'docker build -t ' + imageName + ':' + image + '-8 -f ' + image + '/Dockerfile ' + image
    }
  }

  images.each {
    image -> stage( 'Publish Java8 ' + image ) {
      sh 'docker push ' + imageName + ':' + image + '-8'
    }
  }

}
