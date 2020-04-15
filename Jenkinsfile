#!groovy
@Library('jenkinslib') _
def tools = new org.devops.tools()
String workspace = "/opt/jenkins/workspace"

pipeline {
   agent { node {label "build01" //指定运行节点的标签或名称
                customWorkspace "${workspace}" //指定运行工作目录（可选）
         }
    }
         
   options {
       timestamps() //日志显示时间
       skipDefaultCheckout()  //删除隐式 checkout scm 语句
       disableConcurrentBuilds() //禁止并行
       timeout(time: 1, unit: 'HOURS') //流水线超时设置1小时
   }
   
   stages {
     //下载代码
      stage('GetCode') { //阶段名称
         steps { //步骤
             timeout(time: 5, unit: "MINUTES"){ //步骤超时时间
                 script{ //填写运行代码
                     print('获取代码')
                }
         }
      }
}   
     //构建
      stage('Build') {
         steps {
             timeout(time: 20, unit: "MINUTES"){
                 script{
                     print('应用打包')
                }
         }
      }
   }
    //代码扫描
      stage('CodeScan') {
         steps {
             timeout(time: 30, unit: "MINUTES"){
                 script{
                     print('代码扫描')
                     tools.PrintMes("This is my lib!")
                }
         }
      }
  }
}

  //构建后操作
     post {
        always{ //总是执行脚本片段
            script{
                println("always")
            }
        }
        
        success{ //成功后执行
            script{
                currentBuild.description = "\n 构建成功!"
            }
        }
        
        failure{ //失败后执行
            script{
                currentBuild.description = "\n 构建失败!"
            }
        }
        
        aborted{ //取消后执行
            script{
                currentBuild.description = "\n 构建取消!"
            }
        }
    }
}
