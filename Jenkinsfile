node('docker'){
    stage('prepare'){
        echo 'Prepare...'
    }
    
    stage('Build ES docker'){
        sh 'docker pull 192.168.84.23:5000/library/elasticsearch:dcos-5.0.2'
        sh 'docker run -itd --name rainbow-es --network bridge -p 9201:9200 -e CLUSTER_NAME=pool -e NODE_NAME=es1 -e NODE_MASTER=true -e PUBLISH_HOST=172.17.0.1 -e HTTP_PORT=9200 -e TCP_PORT=9300 -e PING_UNICAST_HOSTS=172.17.0.1:9300 192.168.84.23:5000/library/elasticsearch:dcos-5.0.2'
    }
    
    stage('Build Rainbow docker'){
        sh 'docker volume create maven-repo'
        sh 'docker pull 192.168.84.23:5000/library/anyrobot-graph-baseimage:dev'
        withDockerContainer(args: "--name build-rainbow -v maven-repo:/root/.m2", image: "192.168.84.23:5000/library/anyrobot-graph-baseimage:dev") {
            echo "WORKSPACE is $WORKSPACE"
            sh 'pip install elasticsearch'
        }   
    }
    
    stage('Clean'){
        echo 'Testing...'
    }
    stage('Deploy'){
        echo 'Deploying...'
    }
}