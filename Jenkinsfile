pipeline {
  agent any
  stages {
    stage('Copy Artifacts') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          def ver = data['3.11.0'].buster
          
          println "ver.project[0] = ${ver.project[0]}"
          println "ver.branch = ${ver.branch}"
          println "ver.project/ver.branch = $ver.project/$ver.branch"
          
          copyArtifacts(projectName: "$ver.project/$ver.branch",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
