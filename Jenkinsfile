pipeline {
agent any


stages {
    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Validate Application') {
        steps {
            sh 'test -f index.html'
            echo 'Employee Management Dashboard HTML file exists.'
        }
    }

    stage('Build') {
        steps {
            echo 'Build completed successfully.'
        }
    }
}

post {
    success {
        echo 'Employee Management Dashboard pipeline completed successfully.'
    }
    failure {
        echo 'Pipeline failed. Check the console output.'
    }
}


}

