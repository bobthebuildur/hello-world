pipeline {
  agent any
    environment {
        VERSION = buildVersionString()
    }
  stages {
    stage("Checkout SCM") {
      steps {
        echo '************* Code Checkout started ************* >'
        git branch: 'main', credentialsId: 'gitubcred', url: 'https://github.com/bobthebuildur/hello-world.git';
        echo '<************* Checkout completed *************>'

      }
    }
    stage("Maven Build") {
      steps {
        echo "************* Building application version ${VERSION} ************* >"
        sh "mvn clean install"
        echo '<************* Build completed *************>'

      }
    }
    stage("Create Docker Image") {
      steps {
        echo "************* Creating Docker Image ${VERSION}************* >"
        sh "sudo docker build -t hello-world:${VERSION} ."
        echo '<************* Build completed *************>'

      }
    }
    stage("Start Containers") {
      steps {
        echo '<************* Starting Container *************>'
        sh "docker run -d --name mycontainer -p 8080:4287 hello-world:${VERSION} "
        echo '<************* Container started  *************>'

      }
    }
  }
}
def buildVersionString() {
    return '1.0_' + env.BUILD_NUMBER
}
