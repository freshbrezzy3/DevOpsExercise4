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
      claimName: 'custom-java-build-storage',
      readOnly: false
      )
  ]) 
{
  node(POD_LABEL) {
    stage('Build Java App') {
      git url: 'https://github.com/junit-team/junit5.git', branch: 'main'
      container('maven') {
        sh 'mvn -B -ntp clean test'
      }
    }
  }
}

