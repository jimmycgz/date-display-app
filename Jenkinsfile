node() {
    echo "Your Pipeline works!"
    //sh('ls -la')
    
    Stage('Checkout SCM') {
        checkout($class:'GitSCM')
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
