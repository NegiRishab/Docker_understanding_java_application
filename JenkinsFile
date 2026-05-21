def gv

pipeline {

    agent any
    tools {
        maven 'maven-3.9' 
    }

    stages {
        stage('init') {
            steps {
                echo 'Initializing...'
                script {
                    gv = load 'script.groovy'
                }
            }
        }
        stage('Increment Build Number') {
            steps {
                gv.incrementBuildNumber()
            }
        }
        stage('Build') {
            steps {
                gv.build()
            }
        }
        stage('Test') {
            steps {
                gv.test()
            }
        }
        stage('Build Image') {
            when{
                expression { return env.BRANCH_NAME == 'main' }
            }
            steps {
                gv.buildImage()
            }
        }
        stage('Deploy') {
            steps {
                gv.deploy()
            }
        }
        stage('git') {
            when{
                expression { return env.BRANCH_NAME == 'main' }
            }
            steps {
                gv.git()
            }
        }
    }
    post {
      
        success {
            echo 'This will run only if the stages succeed.'
        }
        failure {
            echo 'This will run only if the stages fail.'
        }
    }
}