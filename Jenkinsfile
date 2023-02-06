def CONTAINER_NAME="hello-world"
def CONTAINER_TAG="latest"
def IMAGE_NAME="mycontiner"
def IMAGE_VERSION


pipeline {
  agent any
    environment {
        VERSION = buildVersionString()
    }
  stages {
  
    stage("Maven Build") {
      steps {
        echo "************* Building application version ${VERSION} ************* >"
        sh "/opt/maven/bin/mvn clean install"
        echo '<************* Build completed *************>'

      }
    }
    stage("Create Docker Image") {
      steps {
        echo "************* Creating Docker Image ${VERSION}************* >"
        sh "docker build -t $IMAGE_NAME:${VERSION} ."
        echo '<************* Build completed *************>'

      }
    }
    stage("Containers Initialization") {
      steps {
 
        echo '<************* Stopping old Container *************>'
        sh "docker stop $CONTAINER_NAME"
        sh "docker rm $CONTAINER_NAME"
        echo '<************* Old container stopped *************>'
        
        echo '<************* Starting Container *************>'
        sh "docker run -d --name $CONTAINER_NAME -p 4287:4287 $IMAGE_NAME:${VERSION} "
        echo '<************* Container started  *************>'

      }
    }
  }
}
def buildVersionString() {
    return '1.0_' + env.BUILD_NUMBER
}
