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
                echo 'Hello World 15'
            }
        }
    }

    post {
        success {
            script {
                println env.BRANCH_NAME
                if(env.BRANCH_NAME == 'main') {
                    sh "echo ${GIT_COMMIT} > COMMIT_HASH"
                    writeFile file: 'COMMIT_HASH2', text: ${GIT_COMMIT}"
                    build(job: 'benedek.izso.test', wait: false, parameters: [string(name: 'ENV', value: 'staging')])
                }
            }
        }
    }
}