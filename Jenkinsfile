 @Library('pipeline-library-demo')_

 stage('Demo') {
     echo 'Hello world'
     sayHello 'sudheer'
 }
 stage('test')
     wget https://github.com/aquasecurity/trivy/releases/download/v0.20.1/trivy_0.20.1_Linux-64bit.deb
     sudo dpkg -i trivy_0.20.1_Linux-64bit.deb
     checkout
     docker pull "${DOCKER_USERNAME}"/test:1.0.0
     trivy image --severity HIGH,CRITICAL "${DOCKER_USERNAME}"/test:1.0.0
