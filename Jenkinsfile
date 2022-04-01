pipeline { /* os estágios da pipeline estarão nesse bloco */
    agent any /* agente é 'quem' vai executar a pipeline */

    stages { /* inicia a criação das etapas */
        stage('Checkout Source') { /* primeira etapa */
            steps { /* define os passos a serem executados nessa etapa */
                git url:'https://github.com/daniel10-souza/rotten-potatoes.git', branch: 'main' /* 'pega' a fonte do projeto */
            }
        }

        stage('Build Image') { /* segunda etapa */
            steps {
                script {
                    dockerapp = docker.build("daniel10souza/rotten-potatoes:${env.BUILD_ID}",
                      '-f ./src/Dockerfile .') /* comando de criação da imagem */
                }                 
            }
        }

        stage('Push Image') {
            steps {
                script { /* registra no docker hub com a credencial criada no Jenkins, em seguida, faz o push das duas imagens */
                        docker.withRegistry('https://registry.hub.docker.com', 'docker_hub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
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

                    kubernetesDeploy(configs: '**/k8s/**', kubeconfigId: 'kubeconfig') /*faz o deploy, utilizando a credencial do kubeconfig no Jenkins e passando a pasta com os manifestos*/
                }
            }
        }
    }
}