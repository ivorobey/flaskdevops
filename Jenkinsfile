Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@ivorobey 
buldozer231
/
spring-boot
forked from spring-projects/spring-boot
0
031.8k
Code
Pull requests
Actions
Projects
Wiki
Security
Insights
spring-boot/Jenkinsfile
@buldozer231
buldozer231 test
Latest commit 84cddce on 1 Dec 2019
 History
 1 contributor
63 lines (56 sloc)  2.01 KB
  

def REPO_URL = "https://github.com/buldozer231/spring-boot/"
def POM_PATH = "spring-boot/spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui/pom.xml"
def BUILD_VERSION = '1.0.'+env.BUILD_NUMBER
def IMAGE_PATH    = 'spring-boot/spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui/target/spring-boot-smoke-test-web-ui-2.2.1.BUILD-SNAPSHOT.jar'
def ARTIFACT_ID = "spring-boot"
def NEXUS_REPO = "maven-releases"
def NEXUS_URL = "34.70.39.207"
def NEXUS_PORT = "80"
def NEXUS_GROUP = "graduation"
def ARTIFACT_NAME = "spring-boot"


withCredentials([usernameColonPassword(credentialsId: 'e56b0ea0-d636-4532-9f7a-8e542fa16760', variable: 'nexus')]) {
        // some block
}

node () {
    stage ("CHECKOUT") {
        //    sh "pwd"
        sh "rm -rf spring-boot/"
        sh "git clone ${REPO_URL}"
    }
    stage ("BUILD") {
       withMaven(
            maven: 'maven') {
            sh "mvn clean install -e -f ${POM_PATH}"
        }
    }
    stage ("UPLOAD ARTIFACT") {
        nexusArtifactUploader(
            nexusVersion: 'nexus3',
            protocol: 'http',
            nexusUrl: "${NEXUS_URL}:${NEXUS_PORT}",
            groupId: "${NEXUS_GROUP}",
            version: "${BUILD_VERSION}",
            repository: "${NEXUS_REPO}",
            credentialsId: 'e56b0ea0-d636-4532-9f7a-8e542fa16760',
            artifacts: [
                [artifactId: "${ARTIFACT_ID}",
                classifier: '',
                file: "${IMAGE_PATH}",
                type: 'jar']
            ]
        )
    }

    stage ("Build Docker image") {
//          sh "sudo -i"
        sh "cp ${IMAGE_PATH} /var/lib/jenkins/docker-tmp/"
        sh "cd /var/lib/jenkins/workspace/graduation/spring-boot/ansible && ansible-playbook -l dev-tools playbooks/build-image.yml --tags deploy"
     }
    //   34.70.39.207/repository/
    //maven-releases/Graduation/spring-boot/1.0.48/spring-boot-1.0.48.jar

    stage ("CI DEPLOY") {
        build 'CI-deploy'
    }
    stage ("QA DEPLOY") {
        build 'QA-deploy'
    }

}
© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
