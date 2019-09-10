pipeline {
  agent any
  stages {
    stage('Read File') {
      steps {
        script {
          def data = readJSON file: 'test.json'
          def myList = data['list']
        }

        echo "${myList[0].letter} = ${myList[0].number}"
        echo "${myList[1].letter} = ${myList[1].number}"
        echo "${myList[2].letter} = ${myList[2].number}"

      }
    }
    stage('Output Stuff') {
      steps {
        echo "${myList[0].letter} = ${myList[0].number}"
        echo "${myList[1].letter} = ${myList[1].number}"
        echo "${myList[2].letter} = ${myList[2].number}"
      }
    }
  }
}
