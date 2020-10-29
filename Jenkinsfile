withCredentials([sshUserPrivateKey(credentialsId: '215c0426-5204-426e-8a8a-49209334fb91', keyFileVariable: '', passphraseVariable: '', usernameVariable: '')]) {
    // some block
}
node () {
    stage ("CHECKOUT") {
        sshagent (credentials: ['215c0426-5204-426e-8a8a-49209334fb91']) {
        sh 'ssh -o StrictHostKeyChecking=no -l cloudbees ec-2@ec2-53-187-240-52.us-west-2.compute.amazonaws.com uname -a'
  }
    }
}