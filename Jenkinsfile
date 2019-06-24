node('master') {
    stage('init') {
        checkout scm
    }

    stage('image build') {
        sh '''
            ./mvnw clean package
            mv target/*.jar petclinic.jar
            zip petclinic.zip web.config petclinic.jar
        '''
    }

    stage('preview') {
        azureWebAppPublish appName: env.APP_NAME,
            azureCredentialsId: env.CRED_ID,
            resourceGroup: env.RESOURCE_GROUP,
            filePath: '*.zip'
    }
}