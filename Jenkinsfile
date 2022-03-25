pipeline { /* os estágios da pipeline estarão nesse bloco */
    agent any /* agente é 'quem' vai executar a pipeline */

    stages { /* inicia a criação das etapas */
        stage('Checkout Source') { /* primeira etapa */
            steps { /* define os passos a serem executados nessa etapa */
                git url:'https://github.com/daniel10-souza/rotten-potatoes.git', branch: 'main' /* 'pega' a fonte do projeto */
            }         
        }

        stage('Deploy Kubernetes') {
            agent { /*Define um novo agente para excutar o deploy*/
                kubernetes {
                    cloud 'kubernetes' /*nome do cloud provider*/
            } 
            steps {
                script {
                    kubernetesDeploy(configs: "**/k8s/**", kubeconfigId: "kubeconfig") /*faz o deploy, utilziando a credencial do kubeconfig no Jenkins e passando a pasta com os manifestos*/
                }
            }
    }
}