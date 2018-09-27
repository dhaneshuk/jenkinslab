pipeline {
  agent any
  stages {
    stage('Stage1') {
      parallel {
        stage('Stage1') {
          agent any
          steps {
            sh '''echo $test
#Memory Usage
ssh test@192.168.43.46 free | grep Mem | awk \'{print $3/$2 * 100.0}\'
#Swap Usage
ssh test@192.168.43.46 free | grep Swap | awk \'{print $3/$2 * 100.0}\'

#Disk Space
ssh test@192.168.43.46 df -hT|grep -v tmpfs|awk \'{print $1,$7,$6}\'

#CPU Usage
ssh test@192.168.43.46 grep \'cpu \' /proc/stat | awk \'{usage=($2+$4)*100/($2+$4+$5)} END {print usage "%"}\'
ssh test@192.168.43.46 top -bn1 | grep "Cpu(s)" | sed "s/.*, *\\([0-9.]*\\)%* id.*/\\1/" | awk \'{print 100 - $1"%"}\''''
          }
        }
        stage('stage1_2') {
          steps {
            sh 'echo "testing again $test"'
          }
        }
      }
    }
    stage('Stage2') {
      steps {
        mail(subject: 'Test', body: 'Test Mail', from: 'jenkins@mydesk.com', to: 'dhaneshnarayanan@gmail.com')
      }
    }
  }
  environment {
    test = 'test1'
  }
}