   pipeline {
  agent any

  tools {
    // Nombre dado a la instalación de Maven en "Tools configuration"
    maven "Default Maven"
  }

  stages {
    stage('Git fetch') { 
      steps {
        // Get some code from a GitHub repository
        git branch: 'main', url: 'https://github.com/ualhmis/MavenEjercicios'
      }
    }
    stage('Compile, Test, Package') { 
      steps {
        // When necessary, use '-f path-to/pom.xml' to give the path to pom.xml
        // Run goal 'package'. It includes compile, test and package.
        sh "mvn  -f sesion07Maven/pom.xml clean package" 
      }
      post { 
        // Record the test results and archive the jar file.
        success {
          junit '**/target/surefire-reports/TEST-*.xml'
          archiveArtifacts '**/target/*.jar'
        }
      }
    }
  }
}
  success { 
    junit '**/target/surefire-reports/TEST-*.xml'
    archiveArtifacts '**/target/*.jar'
    jacoco( 
      execPattern: '**/target/jacoco.exec',
      classPattern: '**/target/classes',
      sourcePattern: '**/src/',
      exclusionPattern: '**/test/'
    )
    publishCoverage adapters: [jacocoAdapter('**/target/site/jacoco/jacoco.xml')] 
  }


  segundo cambio

  cambio 1 rama1
  cambio2 rama1

  cambio1 rama2