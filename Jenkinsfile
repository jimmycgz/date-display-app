node() {
    echo "Your Pipeline works!"
    //sh('ls -la')
    
    stage('Checkout SCM') {
        def scmVars = checkout scm
        def commitHash = scmVars.GIT_COMMIT
        echo 'chk out done!' 
    }
    
    stage('Build') {
            steps {
                echo 'Building..'
                docker { image 'node:carbon-jessie' }
            }
        }
    
     stage('Test') {
            steps {
                echo 'Testing..'
                sh('npm test')
            }
        }
    
      stage('Deploy-push') {
            steps {
                echo 'Deploying....'
            }

}
} 
