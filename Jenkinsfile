pipeline {
  agent any
  stages {
    stage('Build&Test') {
      agent {
        node {
          label 'docker-1'
        }

      }
      steps {
        sh 'mvn clean package'
        stash(name: 'build-test-aritfacts', includes: 'target/*.jar, target/surefire-reports/TEST-*.xml', allowEmpty: true)
      }
    }
    stage('Report & Publish') {
      agent {
        node {
          label 'docker-1'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit(testResults: '**/target/surfire-reports/TEST-*.xml', allowEmptyResults: true)
        archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true)
      }
    }
  }
}