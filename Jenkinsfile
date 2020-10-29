
def REPO_URL = "https://github.com/ivorobey/flaskdevops"
node (){
  stage ("CHECKOUT") {
        sh "rm -rf flaskdevops/"
        sh "git clone ${REPO_URL}"
        sh 'sudo rsync  -e "ssh -i /root/.ssh/id_rsa" -r flaskdevops/app/ ubuntu@ec2-54-187-240-52.us-west-2.compute.amazonaws.com:/opt/app'
        sh 'ssh ubuntu@ec2-54-187-240-52.us-west-2.compute.amazonaws.com uname -a'
  }
}








// node () {
//     stage ("CHECKOUT") {
//         sshagent (credentials: ['215c0426-5204-426e-8a8a-49209334fb91']) {
//         sh 'ssh -o StrictHostKeyChecking=no -l cloudbees ec-2@ec2-53-187-240-52.us-west-2.compute.amazonaws.com uname -a'
//   }
//     }
// }