pipeline {

environment {
     timeout_for_notepad_watcher = 120
   }

    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test On thinkpad') {
                    agent {
                        label "master"
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
                        bat "calc.exe"
                    }
                    post {
                        always {
                            println "hello akoya"
                        }
                    }
                }
            }
        }
    }
}
