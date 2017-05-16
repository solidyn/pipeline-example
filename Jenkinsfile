#!/usr/bin/env groovy
node() {
  stage('Checkout Code') {
    checkout scm
  }
  
  stage('Syntax Checks') {
    echo "Checking files..."
    sleep 11
  }
  
  stage('Compile') {
     echo 'Compiling...'
     sleep 23
  }
  
  stage('Unit Tests') {
    dir('reports') {
      echo "Running unit tests..."
      sleep 15
      writeFile file: 'test.xml', text: '''
<testsuite tests="3">
    <testcase classname="foo1" name="ASuccessfulTest"/>
    <testcase classname="foo2" name="AnotherSuccessfulTest"/>
    <testcase classname="foo3" name="AFailingTest">
        <failure type="NotEnoughFoo"> details about failure </failure>
    </testcase>
</testsuite>
      '''
    }
    step([$class: 'XUnitBuilder', testTimeMargin: '3000', thresholdMode: 1, 
      thresholds: [[$class: 'FailedThreshold', failureNewThreshold: '1', failureThreshold: '1', unstableNewThreshold: '1', unstableThreshold: '1'], 
      [$class: 'SkippedThreshold', failureNewThreshold: '1', failureThreshold: '1', unstableNewThreshold: '1', unstableThreshold: '1']], 
      tools: [[$class: 'JUnitType', deleteOutputFiles: true, failIfNotNew: false, pattern: 'reports/**/*.xml', skipNoTestFiles: true, stopProcessingIfError: true]]])
  }
  
  stage('Deploy to Integration') {
    echo "Deploying..."
    sleep 10
  }
}
