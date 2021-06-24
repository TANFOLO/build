node{
    def registryProjet='registry.gitlab.com/tanfolo/jenkins'
    def IMAGE='${registryProjet}:version-${env.BUILD_ID}'
    stage('Clone'){
        git 'https://github.com/TANFOLO/build.git'
    }
    
    def img = stage('Build'){
        docker.build("$IMAGE", '.');
    }
    
    stage('Run'){
        img.withRun("--name run-$BUILD_ID -p 80:80"){ c ->
            bat 'curl localhost'
            
        }
    }
    stage('Push'){
        docker.withRegistry('https://registry.gitlab.com', 'reg1'){
            img.push 'latest'
            imh.push()
        }
    }
}