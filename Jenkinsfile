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
      <?xml version="1.0" encoding="UTF-8"?>
      <testsuites>
         <testsuite name="JUnitXmlReporter" errors="0" tests="0" failures="0" time="0" timestamp="2013-05-24T10:23:58" />
         <testsuite name="JUnitXmlReporter.constructor" errors="0" skipped="1" tests="3" failures="1" time="0.006" timestamp="2013-05-24T10:23:58">
            <properties>
               <property name="java.vendor" value="Sun Microsystems Inc." />
               <property name="compiler.debug" value="on" />
               <property name="project.jdk.classpath" value="jdk.classpath.1.6" />
            </properties>
            <testcase classname="JUnitXmlReporter.constructor" name="should default path to an empty string" time="0.006">
               <failure message="test failure">Assertion failed</failure>
            </testcase>
            <testcase classname="JUnitXmlReporter.constructor" name="should default consolidate to true" time="0">
               <skipped />
            </testcase>
            <testcase classname="JUnitXmlReporter.constructor" name="should default useDotNotation to true" time="0" />
         </testsuite>
      </testsuites>
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
