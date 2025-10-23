// Triggert automatisch bij elke push (Poll SCM: elke minuut)
properties([pipelineTriggers([pollSCM('* * * * *')])])

pipeline {
  agent any

  stages {
    stage('Preparation') {
      steps {
        // Oude container weg (fout negeren als hij niet bestaat)
        sh 'docker rm -f samplerunning || true'
      }
    }

    stage('Build') {
      steps {
        // Gebruik je bestaande Freestyle job
        build job: 'BuildSampleApp', wait: true, propagate: true
      }
    }

    stage('Results') {
      steps {
        // Gebruik je bestaande Test job
        build job: 'TestSampleApp', wait: true, propagate: true
      }
    }
  }
}
