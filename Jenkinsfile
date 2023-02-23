pipeline {
    environment {
        http_proxy = 'http://webproxy.emarsys.at:3128'
        https_proxy = 'http://webproxy.emarsys.at:3128'
        
        FULL_PATH_BRANCH = sh(returnStdout: true, script: "git name-rev --name-only HEAD | xargs | tr -d '\n'").trim()
        BRANCH_NAME = FULL_PATH_BRANCH.substring(FULL_PATH_BRANCH.lastIndexOf('/') + 1, FULL_PATH_BRANCH.length())
    }
    
    agent any
 
    stages {
        stage('Greeting') {
            steps {
                echo 'Hello World 27'
            }
        }
    }

    post {
        success {
            script {
                println env.BRANCH_NAME
                if(env.BRANCH_NAME == 'main') {
                    writeFile file: 'COMMIT_HASH', text: env.GIT_COMMIT
                    archiveArtifacts artifacts: 'COMMIT_HASH', fingerprint: true
                    build(job: 'benedek.izso.test', wait: false, parameters: [string(name: 'ENV', value: 'staging')])
                }
            }
        }
    }
}