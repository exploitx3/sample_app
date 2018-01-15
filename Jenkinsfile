#!groovy

properties(
    [
        [$class: 'BuildDiscarderProperty', strategy:
          [$class: 'LogRotator', artifactDaysToKeepStr: '14', artifactNumToKeepStr: '5', daysToKeepStr: '30', numToKeepStr: '60']],
        pipelineTriggers(
          [
              pollSCM('H/15 * * * *'),
              cron('@daily'),
          ]
        )
    ]
)
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'rvm use 1.9.3'
                sh 'bundle install'
            }
        }
        stage('Test') {
            steps {
                sh 'rake spec'
            }
        }
    }
}
