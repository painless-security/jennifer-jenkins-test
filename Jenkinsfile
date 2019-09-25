def psecUpstreams = "eapol-test/jennifer%2Fjenkins, moonshot-ms-infrastructure/jennifer%2Fjenkins"
pipeline {
  agent {
    label 'deb-repository'
  }
  
  parameters {
    booleanParam(name: 'RELEASE', defaultValue: false, description: 'Build for release')
    string(name: 'VERSION', defaultValue: 'v3.12.0', description: 'Version to build')
  }
  
  environment {
    // Extract the portion of our project name after the slash
    PSEC_SUBPROJECT_NAME = """${sh(
      returnStdout: true,
      script: 'echo \$JOB_NAME | sed s,[^/]*/,,'
    )}"""
    TEST='yep'
  }
  
  triggers {
    upstream(
      upstreamProjects: """${
        [
          "projectA/${env.BRANCH_NAME}",
          "projectB/${env.BRANCH_NAME}"
        ].join(',').replaceAll('/','%2F')
      }""",
      threshold: hudson.model.Result.SUCCESS
    )
  }
  
  stages {
    stage('Initialization') {
      steps {
        script {
          // Read configuration
          psecBuildConfig = readYaml file: 'config.yml'
        }
      }
    }
    
    stage('Build repository') {
      steps {
        script {
          for (upstream in psecBuildConfig.upstream_projects) {
            // Get specified branch or fall back to the branch of the
            // current build, then replace '/' with the URL-ified equivalent.
            String branch = upstream.get(
                              'branch', env.BRANCH_NAME
                            ).replaceAll('/', '%2F')

            // Copy artifacts from the requested project/branch
            copyArtifacts(
              projectName: "${upstream.name}/${branch}",
              target: 'incoming-debs/',
              selector: lastSuccessful()
            )
          }
        }
      }
    }
  }
  
//  post {
//   success {
//      archiveArtifacts(
//        artifacts: 'debian-repository-*.tgz'
//      )
//    }
//  }
}
