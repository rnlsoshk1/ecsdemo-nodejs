podTemplate(
	label: 'mypod',
	volumes: [
		emptyDirVolume(mountPath: '/etc/gitrepo', memory: false),
		hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
	],
	containers:
	[
	    containerTemplate(name: 'git', image: 'alpine/git', ttyEnabled: true, command: 'cat'),
	    // containerTemplate(name: 'nodejs', image: 'NodeJS', command: 'cat', ttyEnabled: true),
	    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true,
	    	envVars: [secretEnvVar(key: 'DOCKER_HUB_PASSWORD', secretName: 'docker-hub-password', secretKey: 'DOCKER_HUB_PASSWORD')]
	    ),
        containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm', command: 'cat', ttyEnabled: true),
        containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl', command: 'cat', ttyEnabled: true)
    ]
)
{
    node('mypod') {
        // stage('Clone repository') {
        //     container('git') {
        //         sh 'git clone -b master https://github.com/rnlsoshk1/ecsdemo-nodejs.git /etc/gitrepo'
        //     }
        // }

        // stage('Test source codes') {
        //     container('nodejs') {
        //         sh 'npm install'
        //         sh 'node /etc/gitrepo/test/test.js'
        //     }
        // }

        // stage('Build and push docker image'){
        //     container('docker') {
        //         sh 'docker login -urnlsoshk1 -p$DOCKER_HUB_PASSWORD'
        //         sh 'docker build /etc/gitrepo/ -t rnlsoshk1/nodejs --no-cache'
        //         sh 'docker push rnlsoshk1/nodejs'
        //     }
        // }
        // stage('Build and push helm chart'){
        //     container('helm') {
        //         println "initiliazing helm client"
        //         sh "helm init"
        //         println "checking client/server version"
        //         sh "helm version"

        //         println "Add repository"
        //         sh "helm repo add chartmuseum http://34.85.30.191:8080/"
        //         sh "helm repo update"
        //         sh "[ ! -z \"\$(helm ls msa)\" ] || helm del --purge msa"
        //         println "Running deployment"
        //         sh "helm install chartmuseum/msa"
        //     }
        // }
        stage('kubectl test') {
            container('kubectl'){
                println "kubectl test"
                sh "kubectl create clusterrolebinding default-admin --clusterrole cluster-admin --serviceaccount=default:default"
		sh "kubectl get nodes"
            }
        }
        stage('Helm test') {
            container('helm'){
                println "helm test"
                sh "helm init"
            }
        }
    }
}
