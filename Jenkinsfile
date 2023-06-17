pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = '<user_name>'
        NEXUS_PASS = '<password>'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.10.139'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages {
        stage('Build') {
                    steps {
                        sh 'mvn -s settings.xml -DskipTests install'
                    }
                    post {
                        success {
                            echo "Now Archiving."
                            archiveArtifacts artifacts: '**/*.war'
                        }
                    }
                }

        stage('Test') {
                steps {
                    sh 'mvn test'
                }
                }
            
            stage('Checkstyle Analysis'){
                    steps {
                        sh 'mvn -s settings.xml checkstyle:checkstyle'
                        }
                    }
                }
}
