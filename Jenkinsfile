pipeline {
    environment {
        http_proxy = 'http://webproxy.emarsys.at:3128'
        https_proxy = 'http://webproxy.emarsys.at:3128'
    }
    
    agent any
 
    stages {
        stage('Greeting') {
            steps {
                echo 'Hello Workd'
            }
        }
    }

    post {
        success {
            script {
                if(env.BRANCH_NAME == 'main') {
                    build(job: 'benedek.izso.test', wait: false, parameters: [string(name: 'ENV', value: 'staging')])
                }
            }
        }
    }
}