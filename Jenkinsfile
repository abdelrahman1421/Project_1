/* groovylint-disable-next-line CompileStatic */
pipeline {
    stages {
        stage('Build Docker Image') {
            steps {
                script{
                    /* groovylint-disable-next-line NestedBlockDepth */
                    if (env.BRANCH_NAME == 'master') {
                    /* groovylint-disable-next-line LineLength, NestedBlockDepth */
                        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh """
                                    docker build -f App/html/dockerfile . -t engboda/project:${BUILD_NUMBER}
                                    docker login -u ${USERNAME} -p ${PASSWORD}
                                    docker push engboda/project:${BUILD_NUMBER}
                                    echo ${BUILD_NUMBER} > ../vars.txt

                                """
                        }
                    }
                }
            }
        }
    // stage('Deploy') {
    //     steps {
    //         script {
    //         withCredentials([file(credentialsId: 'kubeconfig', variable: 'FILE')]) {
    //         if (env.BRANCH_NAME == "dev" || env.BRANCH_NAME == "test" || env.BRANCH_NAME == "prod") {
    //             sh """
    //              export NUMBER=\$(cat ../vars.txt)
    //              cp Deployment/deploy.yaml Deployment/deploy.yaml.tmp
    //              cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
    //              rm -f Deployment/deploy.yaml.tmp
    //              kubectl apply -f Deployment/deploy.yaml --kubeconfig=${FILE}
    //              kubectl apply -f Deployment/service.yaml --kubeconfig=${FILE}
    //              """
    //             }
    //         }
    //       }
    //     }
    // }
    }
}