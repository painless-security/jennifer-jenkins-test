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
          ver = data['3.11.0'].buster[0]
          println "data.cat = ${data.cat}"
          println "data.dog = $data.dog"
          println "data.frog = $data.frog"
        }
      }
    }
    
    stage('Copy artifact') {
      steps {
        script {
          println "ver.project = ${ver.project}"
          println "ver.branch = ${ver.branch}"
          
          copyArtifacts(projectName: "${ver.project}/${ver.branch.replaceAll('/', '%2F')}",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
