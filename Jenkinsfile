podTemplate(
    containers: [
        containerTemplate(
            name: 'maven',
            image: 'maven:3.8.1-jdk-8', // Adjust the image version as necessary
            command: 'cat',
            ttyEnabled: true,
            volumeMounts: [
                volumeMount(
                    mountPath: '/root/.m2/repository',
                    name: 'maven-repo'
                )
            ]
        )
    ],
    volumes: [
        persistentVolumeClaim(
            claimName: 'maven-pvc', // Ensure this matches the name of your PVC
            mountPath: '/root/.m2/repository',
            readOnly: false
        )
    ]
) {
    node {
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

