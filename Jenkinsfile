def apicEnvs = [:]

pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        durabilityHint('PERFORMANCE_OPTIMIZED')
        disableConcurrentBuilds()
    }

    environment {
        DB_ENGINE    = 'sqlite'
    }

    stages {
        stage('init') {
            steps {
                script{
                    echo "Workspace: ${env.WORKSPACE}"
                    apicEnvs = readProperties file: 'env.properties'
                    echo 'apicEnvs ::: '+ apicEnvs
                    echo "PROP1 :::: ${apicEnvs['testServer']}"
                    echo "PROP2 :::: ${apicEnvs['testProviderOrg']}"
                    echo "PROP3 :::: ${apicEnvs['testCatalog']}"
                }
            }
        }
        stage('connect-to-apic') {
            steps {
                sh "${JENKINS_HOME}/bin/apic login -s ${apicEnvs['devServer']} -u jenkins -p bIdENTaRaLyh"
                echo "Successfully Logged In: ${apicEnvs['devServer']}"
            }
        }
        stage('disconnect-from-apic') {
            steps {
                sh "${JENKINS_HOME}/bin/apic logout -s ${apicEnvs['devServer']}"
                echo "Successfully Logged out: from ${apicEnvs['devServer']}"
            }
        }
    }
}
