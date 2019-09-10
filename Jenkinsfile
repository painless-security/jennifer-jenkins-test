pipeline {
  agent any
  stages {
    stage('Copy Artifacts') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          def ver = data['3.11.0'].buster
          
          copyArtifacts(projectName: "$buster.project/$buster.branch",
                        selector: lastSuccessful())
        }
      }
    }
  }
}
