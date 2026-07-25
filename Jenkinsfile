node{
    def mavenHome=tool name:"maven3.9.10"
    echo "branch name : ${env.NODE_NAME}"
    stage('checkout'){
        git branch: 'development', credentialsId: 'b20ef627-99fd-4ec3-b190-512d9ce819de', url: 'https://github.com/hariiikrishn/Maven-Web-Application.git'
    }
    stage('build'){
        sh "$mavenHome/bin/mvn clean package"
    }
     stage('sonarqube report'){
        sh "$mavenHome/bin/mvn sonar:sonar"
    }
    // stage('upload artifact to nexus'){
    //     sh "$mavenHome/bin/mvn deploy"
    // }
    stage('deploy to tomcat'){
        sshagent(['sshkey']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ubuntu@15.252.17.121:/opt/tomcat/webapps"
        }
    }
}
