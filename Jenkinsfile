pipeline {
    
    // Specify the agent to run the pipeline
    agent any
    // Set environment variables for the pipeline
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    // Define the stages of the pipeline
    stages {
        // Stage for checking out the repository
        stage('GitHub Clone') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/SaiDevOpsFaculty/saidemytrend.git', branch: 'main'
            }
        }

        // Stage for building the project
        stage("build") {
            steps {
                // Run Maven clean and deploy commands
                sh 'mvn clean deploy'
            }
        }

        // Stage for SonarQube analysis
        stage('SonarQube analysis') {
            environment {
                // Set the SonarQube scanner tool
                scannerHome = tool 'saidemy-sonar-scanner'
            }
            steps {
                // Execute SonarQube analysis within the SonarQube environment
                withSonarQubeEnv('saidemy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
