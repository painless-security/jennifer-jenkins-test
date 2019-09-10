pipeline {
  agent any
  stages {
    stage('Copy Artifacts') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          def ver = data['3.11.0'].buster
          
          println "ver.project[0] = ${ver.project[0]}"
          println "ver.branch = ${ver.branch[0]}"
          
          copyArtifacts(projectName: "${ver.project[0]}/${ver.branch[0]}",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
