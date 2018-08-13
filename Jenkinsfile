pipeline {
    agent { label 'master'}
    stages {
      stage('check tools') {
        steps{
            sh "bitrise -v"
            sh "node -v"
            sh "npm -v"
            sh "pip -V"
        }
      }
      stage('test_01') {
        steps {
            script {
                echo "Triggering testing workflow...."
                bitrise_version =sh(returnStdout:true, script: '#!/bin/bash -e \n bitrise -v')?.trim()
                // trigger the workflow              
            }
        }
      }
      stage('build_02') {
        steps {
          script {
            echo "Triggering Buil workflow"
            echo "building......"
          }
        }
      }
      stage('tag_03') {
        steps {
          script {
            echo "Triggering tag workflow"
            echo "tagging .............."
          }
        }
      }
      stage('Deploy_04') {
        when {
          expression {
            return JENKINS_ENVIRONMENT == 'production'
          }
        }
        steps {
            echo "Triggering deploy workflow"
            echo "deploying....."
        }
      }
    }
    post {
      success {
        sh '#!/bin/bash -e \n echo success'
      }
      failure {
        sh '#!/bin/bash -e \n echo failure'
      }
    }
}
