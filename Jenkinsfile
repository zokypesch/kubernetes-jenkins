node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    // tag = "crot"
    appName = "my-jenkins"
    registryHost = "zokypesch/"
    imageName = "${registryHost}${appName}:${tag}"
    env.BUILDIMG=imageName
    env.BUILD_TAG=tag

    stage "Build"
    
        sh "docker build -t ${imageName} -f applications/Dockerfile applications"
    
    stage "Login"
        
        sh "docker login -u="zokypesch" -p="maulanakerenaja""
    
    stage "Push"

        sh "docker push ${imageName}"

    stage "Deploy"

        kubernetesDeploy configs: "applications/k8s/*.yaml", kubeconfigId: 'kubeconfig'

}
