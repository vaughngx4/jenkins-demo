/* 
    Jenkinsfile with badges using https://plugins.jenkins.io/embeddable-build-status/
*/

def buildBadge = addEmbeddableBadgeConfiguration(id: "build", subject: "build")

def status = 'failing'

def RunBuild() {
    echo 'Stage 1 - Building'
    sleep 10
    // Uncomment the line below to test failing build
    // error 'testing failure'
}

def RunTest() {
    echo 'Stage 2 - Testing'
    sleep 10
}

def RunDeploy() {
    echo 'Stage 3 - Deploying'
    sleep 5
}

pipeline {

    agent any

    stages {

        stage('Building') {

            steps {

                script {
                    buildBadge.setStatus('running')
                    try {
                        RunBuild()
                        // buildBadge.setStatus('passing')
                    } catch (Exception err) {
                        buildBadge.setStatus('failing')

                        /* Note: If you do not set the color
                                 the configuration uses the best status-matching color.
                                 passing -> brightgreen
                                 failing -> red
                                 ...
                        */
                      
                        // buildBadge.setColor('pink')
                        error 'Build failed'
                    }
                }
            }
        }

        stage('Testing') {

            steps {

                script {
                    buildBadge.setStatus('running')
                    try {
                        RunTest()
                        buildBadge.setStatus('passing')
                    } catch (Exception err) {
                        buildBadge.setStatus('failing')
                        error 'Test failed'
                    }
                }
            }
        }

        stage('Deploying') {

            steps {

                script {
                    try {
                        RunDeploy()
                    } catch (Exception err) {
                        error 'Deploy failed'
                    }
                }
            }
        }
    }
}
