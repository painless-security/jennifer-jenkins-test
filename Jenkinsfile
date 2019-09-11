pipeline {
  agent any
  stages {
    stage('Read file') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          ver = data['3.11.0'].buster
        }
      }
    }
    
    stage('Copy artifact') {
      steps {
        script {
          println "ver.project[0] = ${ver.project[0]}"
          println "ver.branch = ${ver.branch[0]}"
          
          copyArtifacts(projectName: "${ver.project[0]}/${ver.branch[0]}",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
