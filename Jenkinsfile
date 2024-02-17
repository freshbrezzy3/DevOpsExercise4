podTemplate(
    cloud: 'kubernetes', // Specify your Kubernetes cloud configuration if you have multiple
    containers: [
        containerTemplate(
            name: 'maven',
            image: 'maven:3.8.1-jdk-8',
            command: 'cat',
            ttyEnabled: true
        )
    ],
    volumes: [
        persistentVolumeClaim(
            claimName: 'maven-pvc',
            mountPath: '/root/.m2/repository',
            readOnly: false
        )
    ]
) {
    node(POD_LABEL) {
        stage('Checkout') {
            checkout scm
        }
        stage('Build') {
            container('maven') {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
}

