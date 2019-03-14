def label = "worker-${UUID.randomUUID().toString()}"
podTemplate(label: label, containers: [
      containerTemplate(name: 'npm_j', image: 'node:carbon-jessie', command: 'npm test', ttyEnabled: true)
      //containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
      //containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.8', command: 'cat', ttyEnabled: true),
      //containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:latest', command: 'cat', ttyEnabled: true)
    ],
  
volumes: [
  hostPathVolume(mountPath: '/home/gradle/.gradle', hostPath: '/tmp/jenkins/.gradle'),
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
node(label) {
    echo "Your Pipeline works!"
    //sh('ls -la')
   //def shortGitCommit = "${gitCommit[0..10]}"
    //def previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)
                
    stage('Checkout SCM') {
       def myRepo = checkout scm
       def gitCommit = myRepo.GIT_COMMIT
        def gitBranch = myRepo.GIT_BRANCH
        echo 'chk out done!' 
    }

     stage('Test') {
      try {
        container('npm_j') {
          sh """
            pwd
            echo "GIT_BRANCH=${gitBranch}" >> /etc/environment
            echo "GIT_COMMIT=${gitCommit}" >> /etc/environment
            npm test
            """
        }
      }
      catch (exc) {
        println "Failed to test - ${currentBuild.fullDisplayName}"
        throw(exc)
      }
      }
     
     stage('Deploy-push') {
         container('npm_j') {
        sh "npm build"
      }
     }
      stage('Deploy-push') {

                echo 'Deploying....'

}
} 
} 
