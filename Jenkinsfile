pipeline {
  agent any
  
  environment {
    // Extract the portion of our project name after the slash
    PSEC_SUBPROJECT_NAME = """${sh(
      returnStdout: true,
      script: 'echo \$JOB_NAME | sed s,[^/]*/,,'
    )}"""
  }

  stages {
    stage('Echo stuff') {
      steps {
        echo "${env.PSEC_SUBPROJECT_NAME}"
      }
    }
    
    stage('Read file') {
      steps {
        script {
          def data = readYaml file: 'test.yml'
//          def data = readJSON file: 'test.json'
          ver = data['3.11.0'].buster
        }
      }
    }
    
    stage('Copy artifact') {
      steps {
        script {
          println "ver.project = ${ver.project}"
          println "ver.project[0] = ${ver.project[0]}"
          println "ver.branch = ${ver.branch[0]}"
          
          copyArtifacts(projectName: "${ver.project[0]}/${ver.branch[0].replaceAll('/', '%2F')}",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
