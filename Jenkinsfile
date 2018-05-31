node('docker'){
    stage('Env'){
        echo "WORKSPACE is $WORKSPACE"
    }
    
    stage('Build ES docker'){
		sh 'docker rm -f rainbow-es ||echo'
        sh 'docker pull 192.168.84.23:5000/library/elasticsearch:dcos-5.0.2'
        sh 'docker run -itd --name rainbow-es --network bridge -p 9201:9200 -e CLUSTER_NAME=pool -e NODE_NAME=es1 -e NODE_MASTER=true -e PUBLISH_HOST=172.17.0.1 -e HTTP_PORT=9200 -e TCP_PORT=9300 -e PING_UNICAST_HOSTS=172.17.0.1:9300 192.168.84.23:5000/library/elasticsearch:dcos-5.0.2'
    }
    
    stage('Build Rainbow docker'){
        sh 'docker volume create --name maven-repo'
        sh 'docker pull 192.168.84.23:5000/library/anyrobot-graph-baseimage:dev'
    }
    
    withDockerContainer(args: "--name build-rainbow -v maven-repo:/root/.m2", image: "192.168.84.23:5000/library/anyrobot-graph-baseimage:dev") {
        echo "WORKSPACE is $WORKSPACE"
        sh 'python is_es_start.py'
        sh 'curl -X PUT 172.17.0.1:9201/_template/graph-es -d @template'
    }   
    
    stage('Clean rainbow-es'){
        sh 'docker stop rainbow-es'
		sh 'docker rm -f rainbow-es'
    }
    stage('Deploy'){
        echo 'Deploying...'
    }
}