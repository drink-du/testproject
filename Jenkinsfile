#!groovy
pipeline {
  agent any
  options {
     timeout(time: 1, unit: 'HOURS') 
  }
  parameters {
    string(name: 'PERSON', defaultValue: 'Jenkins', description: 'Who should I say hello to?')
  }
  environment {
      REPOSITORY="ggit@github.com:dujundxh/testproject.git"
  }

  stages {

     stage('获取代码'){
        steps {
            script {
               echo "hello ${params.PERSON}"
               echo "start fetch code from git "
               deleteDir()
               git(
                   branch: "master",
                   url : "${REPOSITORY}",
                   changelog: true
                 )
            }
        }
     }
     
     stage('编译+单元测试'){
        steps {
          script {
             echo "start compile "
             sh "mvn -U -am clean package "
          }
        }        
     }

     stage('Example') {
        try {
            sh 'exit 1'
        }
        catch (exc) {
            echo 'Something failed, I should sound the klaxons!'
            throw
        }
     }
  }


   

  //定义Pipeline或stage运行结束时的操作
  post { 
        always { 
            echo 'I will always say Hello again!'
        }
  }  

}