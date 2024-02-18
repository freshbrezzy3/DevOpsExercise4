podTemplate(containers: [
  containerTemplate(
      name: 'maven', 
      image: 'maven:latest', 
      command: 'sleep', 
      args: '99d'
  )
], 
volumes: [
  persistentVolumeClaim(
      mountPath: '/root/.m2/repository', 
      claimName: 'jhipster-app-storage', 
      readOnly: false
  )
]) 
{
  node(POD_LABEL) {
    stage('Build JHipster Sample App') {
      git url: 'https://github.com/jhipster/jhipster-sample-app.git', branch: 'main'
      container('maven') {
        sh 'mvn -B -ntp clean package -DskipTests'
      }
    }
  }
}

