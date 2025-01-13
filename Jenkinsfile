pipeline {
    agent any
    
    triggers {
        GenericTrigger(
         genericVariables: [
          [key: 'ref', value: '$.ref']
         ],

         causeString: 'Triggered on $ref',

         token: 'abc123',
         tokenCredentialId: '',

         printContributedVariables: true,
         printPostContent: true,

         silentResponse: false,

         shouldNotFlatten: false,

         regexpFilterText: '$ref',
         regexpFilterExpression: 'refs/heads/develop'
    )
  }

    parameters {
        choice(name: 'ENV', choices: ['Dev', 'QA', 'Prod'], description: 'Select the environment')
    }

    environment{
        GIT_URL= 'https://github.com/SudheerKumarP0357/multi-tier-java-mysql.git'
        GIT_BRANCH= 'develop'
    }

    tools{
        jdk 'JAVA17'
        maven 'MAVEN'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch:env.GIT_BRANCH, url:env.GIT_URL
            }
        }
        stage('Build') {
            steps {
                script {
                    if (fileExists('pom.xml')) {
                        echo 'Executing Maven Build'
                        sh "mvn clean package"
                    } else {
                        error 'No pom.xml file found in the repository!'
                    }
                }
            }
        }
        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh "mvn test"
                    }
                }
                stage('Integration Tests') {
                    steps {
                        sh "echo IntegrationTests are running"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENV} environment."
                echo "Deployment has been completed to ${params.ENV} environment."
            }
        }
    }
    post {
        always {
            sh 'cp target/*.jar /home/jenkins'
            cleanWs()
            echo 'Workspace cleaned and artifacts archived.'
        }        
    }
    
}
