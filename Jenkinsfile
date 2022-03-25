pipeline { /* os estágios da pipeline estarão nesse bloco */
    agent any /* agente é 'quem' vai executar a pipeline */

    stages { /* inicia a criação das etapas */
        stage('Checkout Source') { /* primeira etapa */
            steps { /* define os passos a serem executados nessa etapa */
                git url:'https://github.com/daniel10-souza/rotten-potatoes.git', branch: 'main' /* 'pega' a fonte do projeto */
            }         
            }
        }
        stage('Deploy Kubernetes') {
            agent { /*Define um novo agente para excutar o deploy*/
                kubernetes {
                    cloud 'kubernetes' /*nome do cloud provider*/
                }
            }
            environment{
                tag_version = "${env.BUILD_ID}" /* Define a tag a ser usada no deploy da aplicação */
            }
            steps {
                script {
                    sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/api/deployment.yaml' /*insere a tag no arquivo de deployment*/
                    sh 'cat ./k8s/api/deployment.yaml' /*exibe o conteudo para verificar se alterou*/
                    kubernetesDeploy(configs: "**/k8s/**", kubeconfigId: "kubeconfig") /*faz o deploy, utilziando a credencial do kubeconfig no Jenkins e passando a pasta com os manifestos*/
                }
            }
        }
    }
}
