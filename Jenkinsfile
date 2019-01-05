node {
    def ruby2337
    def ruby2338
    def ruby2437
    def ruby2438
    def ruby2537
    def ruby2538
    def ruby2637
    def ruby2638


    docker.withRegistry('', 'dockerwc') {

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

    ruby2337 = docker.build("warecorpdev/base-ruby:2.3-37-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.7-latest ./2.3/alpine3.7/")
    ruby2338 = docker.build("warecorpdev/base-ruby:2.3-38-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.8-latest ./2.3/alpine3.8/")
    ruby2437 = docker.build("warecorpdev/base-ruby:2.4-37-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.7-latest ./2.4/alpine3.7/")
    ruby2438 = docker.build("warecorpdev/base-ruby:2.4-38-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.8-latest ./2.4/alpine3.8/")
    ruby2537 = docker.build("warecorpdev/base-ruby:2.5-37-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.7-latest ./2.5/alpine3.7/")
    ruby2538 = docker.build("warecorpdev/base-ruby:2.5-38-${env.BUILD_ID}", "--build-arg BASE_IMAGE_TAG=3.8-latest ./2.5/alpine3.8/")

    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from alpine38
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('', 'dockerwc') {
            ruby2337.push()
            ruby2338.push()
            ruby2437.push()
            ruby2438.push()
            ruby2537.push()
            ruby2538.push()
            ruby2337.push("2.3-37-latest")
            ruby2338.push("2.3-38-latest")
            ruby2437.push("2.4-37-latest")
            ruby2438.push("2.4-38-latest")
            ruby2537.push("2.5-37-latest")
            ruby2538.push("2.5-38-latest")
        }
    }
    stage('Post') {
    slackSend botUser: true, channel: 'docker-build', message: 'Ruby base image rebuilded', teamDomain: 'warecorp', tokenCredentialId: 'jenkins-token'
  }
}