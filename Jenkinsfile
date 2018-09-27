pipeline {
  agent any
  stages {
    stage('error') {
      agent any
      steps {
        sh '''echo $test
#Memory Usage
free | grep Mem | awk \'{print $3/$2 * 100.0}\'
#Swap Usage
free | grep Swap | awk \'{print $3/$2 * 100.0}\'


#Disk Space
df -hT|grep -v tmpfs|awk \'{print $1,$7,$6}\'

#CPU Usage
grep \'cpu \' /proc/stat | awk \'{usage=($2+$4)*100/($2+$4+$5)} END {print usage "%"}\'
top -bn1 | grep "Cpu(s)" | sed "s/.*, *\\([0-9.]*\\)%* id.*/\\1/" | awk \'{print 100 - $1"%"}\''''
      }
    }
  }
  environment {
    test = 'test1'
  }
}