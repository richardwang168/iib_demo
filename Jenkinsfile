pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        durabilityHint('PERFORMANCE_OPTIMIZED')
        disableConcurrentBuilds()
    }
    stages {
        stage('init') {
            steps {
                script{
                    def apicEnvs = [:]
                    echo "Workspace: ${env.WORKSPACE}"
                    apicEnvs = readProperties file: 'env.properties'
                    echo 'apicEnvs ::: '+ apicEnvs
                    echo "PROP1 :::: ${apicEnvs['devServer']}"
                    echo "PROP2 :::: ${apicEnvs['devProviderOrg']}"
                    echo "PROP3 :::: ${apicEnvs['devCatalog']}"
                    sh "apic login -s ${apicEnvs['devServer']} -u richard.wang@fcl.crs -p Stamina168"
                    echo "Successfully Logged In: ${apicEnvs['devServer']}"
                    sh "apic logout -s ${apicEnvs['devServer']}"
                    echo "Successfully Logged out: from ${apicEnvs['devServer']}"
                }
            }
        }
    }
}
