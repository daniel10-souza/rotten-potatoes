pipeline { /* os estágios da pipeline estarão nesse bloco */
    agent any /* agente é 'quem' vai executar a pipeline */

    stages { /* inicia a criação das etapas */
        stage('Checkout Source') { /* primeira etapa */
            steps { /* define os passos a serem executados nessa etapa */
                git url:'https://github.com/daniel10-souza/rotten-potatoes.git', branch: 'main' /* 'pega' a fonte do projeto */
            }         
        }
    }    
    stages { /* inicia a criação das etapas */
        stage('Deploy-Kubernetes') { /* primeira etapa */
            steps { /* define os passos a serem executados nessa etapa */
               kubernetesDeploy(configs: '**k8s/***', kubeconfigId: 'kubeconfig') /* 'pega' a fonte do projeto */
            }         
        }
    }    
}