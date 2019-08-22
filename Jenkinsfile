pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                echo anil
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "ARTIFACTORY_SERVER",
                    url: "http://13.232.166.108:8081",
                    username: "admin",
                    password: "anil@123",
                    bypassProxy: true
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: "http://13.232.166.108:8081/repository/maven-snapshots/",
                    snapshotRepo: "http://13.232.166.108:8081/repository/maven-snapshots/"
                )

            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean deploy',
                    deployerId: "MAVEN_DEPLOYER",

                )
            }
        }

 
    }
}
