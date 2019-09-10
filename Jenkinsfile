pipeline {
  agent any
  
  stages {
    stage('Read File') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          def myList = data['list']
        }
      }
    }
    
    stage('Output Stuff') {
      steps {
        echo "${list[0].letter} = ${list[0].number}"
        echo "${list[1].letter} = ${list[1].number}"
        echo "${list[2].letter} = ${list[2].number}"
      }
    }
  }
}
