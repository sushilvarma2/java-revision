pipeline {
  agent any
  stages { 
      stage('Unit Test') {
       agent { 
	label 'apache'
	} 
       steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
}

}
  stage('build') {
       agent {
        label 'apache'
        }
 
       steps { 
	sh 'ant -f build.xml -v'
}
}
stage('Deploy') {
       agent {
        label 'apache'
        }
       steps {
       sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangle/all"
}
}
   stage("Running on Centos")
{ 
	agent { 
	  label 'apache'

}
       steps { 
       sh "wget http://varmasushil5.mylabserver.com/rectangle/all/rectangle_${env.BUILD_NUMBER}.jar"
       sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      

}

}

}
  post {
     always { 
       archiveArtifacts artifacts: 'dist/*.jar', fingerprint:true

}

}

}
