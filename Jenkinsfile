pipeline {

environment {
     timeout_for_notepad_watcher = 120
   }

    agent none
    stages {
        stage('start notepad on akoya'){
            agent {
               label "akoya_medion"
            }
            steps {
                    powershell(returnStdout: true, script:'''                            
                        Start-Process -FilePath notepad
                    ''')
            }
                
        }
        stage('Run Tests') {
            parallel {
                stage('this stage succes when no notepad.exe is running on akoya') {
                    agent {
                        label "akoya_medion"
                    }
                    steps {
                        powershell(returnStdout: true, script:"""
               
                            \$ProcessList = \"notepad\"
                            \$timeout_init = 0
                    
                            Do {  
                            
                                    \$ProcessesFound = [bool](Get-Process | ? {\$ProcessList -contains \$_.Name} | Select-Object -ExpandProperty Name)
                                    If (\$ProcessesFound) {
                                        Write-Host \"Still running: \$ProcessesFound\"
                                        Write-Host \"init wait : $timeout_for_notepad_watcher\"
                                        Start-Sleep 1
                                        \$timeout_init++
     
                                    }
                
                                } Until (\$timeout_init -gt $timeout_for_notepad_watcher -or !\$ProcessesFound )
                   
                        """)  
                    }
                    post {
                        always {
                            println "hello thinkpad"
                        }
                    }
                }
                stage('Test On akoya') {
                    agent {
                        label "akoya_medion"
                    }
                    steps {
                        powershell(returnStdout: true, script:"""
                            

                            Start-Sleep 30
                            Stop-Process -name notepad

                        """)
                    }
                    post {
                        always {
                            println "hello akoya"
                        }
                    }
                }
            }
        }
        stage('start notepad on akoya'){
                    agent {
                       label "akoya_medion"
                    }
                    steps {
                            powershell(returnStdout: true, script:'''
                                Start-Process -FilePath notepad
                            ''')
                    }

         }
    }

}
