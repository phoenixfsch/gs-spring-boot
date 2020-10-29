node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         cd complete
         mvn clean package
         cd target
         pwd
         cp ../src/main/resources/web.config web.config
         cp spring-boot-0.0.1-SNAPSHOT.jar app.jar
         zip demoapp.zip app.jar web.config
         pwd
         ls -lah
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}
