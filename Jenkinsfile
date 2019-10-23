pipeline {
    agent any
	 options {
	    disableConcurrentBuilds()
	  }
    stages {
	stage('Running cpp tests') {
		steps {
		  sh '''#!/bin/bash
          mkdir -p build
          cd build
          cmake .. -DUSEXUNIT=ON
          Make -j4
          ./test/aritTest
          '''
		}
	}
    }
  post {
    always {
        xunit(
            thresholds: [ skipped(failureThreshold: '0'), failed(failureThreshold: '0') ],
            tools: [ BoostTest(pattern: 'build/testResult.xml') ])
        )
        cleanWs()
    }
  }
}
