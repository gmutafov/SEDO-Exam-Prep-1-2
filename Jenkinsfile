pipeline {
    agent any

    stages {
        stage('Run only on main or feature branches') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: 'feature/.*', comparator: 'REGEXP'
                }
            }
            stages {
                stage('Checkout') {
                    steps {
                        checkout scm
                    }
                }
                stage('Restore Dependencies') {
                    steps {
                        bat 'dotnet restore'
                    }
                }
                stage('Build') {
                    steps {
                        bat 'dotnet build --no-restore'
                    }
                }
                stage('Test') {
                    steps {
                        bat 'dotnet test --no-build --verbosity normal'
                    }
                }
            }
        }
    }
}
