pipeline {
 agent any
  stages {
    stage('SCM') {
      steps {
         git 'https://github.com/shanmuk98/angular7-sample.git'
       }
    }
   stage("Install node modules") {
     steps {
	     sh 'npm install'
         echo "modules installed"
   }
   }
   stage("build") {
     steps {
			sh 'npm run ng -- build --prod'
            echo "build successful"
   }
   }
}
}
