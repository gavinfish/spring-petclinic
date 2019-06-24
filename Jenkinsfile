node('master') {
    stage('init') {
        checkout scm
    }

    stage('image build') {
        sh "./mvnw package"
        sh "mv target/*.jar target/app.jar"
    }

    stage('preview') {
        azureWebAppPublish appName: env.APP_NAME,
            azureCredentialsId: env.CRED_ID,
            resourceGroup: env.RESOURCE_GROUP,
            filePath: 'target/*.jar'
    }
}