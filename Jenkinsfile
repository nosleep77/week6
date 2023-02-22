pipeline {
     agent any
     triggers {
          pollSCM('* * * * *')
     }

     stages {

          stage("Compile") {
               steps {
                    sh "./gradlew compileJava"
               }
          }

          stage("Unit test") {
            when {
		not {
                branch "main"
		}
            }
               steps {
                    sh "./gradlew test"
               }
          }

          stage("Code coverage") {
	    when {
		branch "main"
	    }
               steps {
                    sh "./gradlew jacocoTestReport"
                    sh "./gradlew jacocoTestCoverageVerification"
               }
          }

          stage("Static code analysis") {
            when {
                not {
                branch "main"
                }
            }
               steps {
                    sh "./gradlew checkstyleMain"
               }
          }

          stage("Package") {
               steps {
                    sh "./gradlew build"
               }
          }

     }
}
