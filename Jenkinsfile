node('docker'){
    stage('prepare'){
        echo 'Prepare...'
    }
    
    stage('While Loop'){
        while(1){
           def count = 0
           echo '${count}'
           count = count + 1
           if(count == 10){
               break
           }
        }
    }
    
    stage('Clean'){
        echo 'Testing...'
    }
    stage('Deploy'){
        echo 'Deploying...'
    }
}