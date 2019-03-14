def label = "worker-${UUID.randomUUID().toString()}"
podTemplate(label: label, containers: [
      containerTemplate(name: 'npmj', image: 'node:carbon-jessie', command: 'cat', ttyEnabled: true)
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
 
    }

     stage('Test') {
      try {
        container('npmj') {
          sh """
		 def myRepo = checkout scm
		 env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
		 def gitCommit = myRepo.GIT_COMMIT
		 echo env.GIT_COMMIT
		 def gitBranch = myRepo.GIT_BRANCH
		 echo "GIT_BRANCH=${gitBranch}" >> /etc/environment
		 echo "GIT_COMMIT=${gitCommit}" >> /etc/environment
		 
		 echo 'chk out done!'
		 pwd
	    

		 npm install
		 npm test
            """
        }
      }
      catch (exc) {
        println "Failed to test - ${currentBuild.fullDisplayName}"
        throw(exc)
      }
      }
     

      


} 
} 
