//variable declaration
// $username = "Administrator"
// $secpass = ConvertTo-SecureString "scgcuAzb&38Df!6WqoVTPwr(nDma)inx" -AsPlainText -Force
// $mycreds = New-Object System.Management.Automation.PSCredential ($username,$secpass)
// $remotepath = "c:\path\to\your.ps1"
// $remoteHostname = "13.56.207.228"
def PowerShell(psCmd) {
    psCmd=psCmd.replaceAll("%", "%%")
    bat "powershell.exe -NonInteractive -ExecutionPolicy Bypass -Command \"\$ErrorActionPreference='Stop';[Console]::OutputEncoding=[System.Text.Encoding]::UTF8;$psCmd;EXIT \$global:LastExitCode\""
}

def cmd_exec(command) {
    return bat(returnStdout: true, script: "${command}").trim()
}

def remoteHostname = "13.56.207.228"
def remoteUsername = "Administrator"
def remotePassword = "scgcuAzb&38Df!6WqoVTPwr(nDma)inx"

def servers = ""
def devServers = ["Test1", "Test2", "Test3"]
def testServers = ["Test1", "Test2", "Test3"]
def ProdServers = ["Test1", "Test2", "Test3"]

properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Env Name from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'environment', 
            randomName: 'choice-parameter-5631314439613978', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Env\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return["Dev","Test","Prod"]'
                ]
            ]
        ], 
        [$class: 'CascadeChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Server from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'server', 
            randomName: 'choice-parameter-5631314456178619', 
            referencedParameters: 'environment', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Environment from Env Param\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        ''' if (environment.equals("Dev")){
                                return["Dev1","Dev2","Dev3"]
                            }
                            else if(environment.equals("Test")){
                                return["Test1","Test2","Test3"]
                            }
                            else if(environment.equals("Prod")){
                                return["Prod1","Prod2","Prod3"]
                            }
                        '''
                ]
            ]
        ],
        choice(name: 'script',
        choices: 'FileCopy',
        description: 'Select script:')
    ])
])

pipeline {
    agent any
    // stages in build pipeline
    stages {
        //first stage
        stage ('Parameter Validation') {
        //steps in test stage
            steps {
                echo 'Checking environment input:'
                echo "Selected: ${params.environment}"
                echo 'Checking server input:'
                echo "Selected: ${params.server}"
                echo 'Checking script input'
                echo "Selected: ${params.script}"
                echo 'Checking username input:'
                echo "Selected: ${params.WindowsUser}"
                echo 'Checking password:'
                echo "Selected: ${params.WindowsPassword}"
            }
        }
        stage ('Execute Script') {
            steps {
                script {
                    if ("${params.environment}" == 'Dev' && "${params.server}" == 'Dev1') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Dev') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Dev' && "${params.server}" == 'Dev2') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Dev') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Dev' && "${params.server}" == 'Dev3') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Dev') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Test' && "${params.server}" == 'Test1') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Test') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Test' && "${params.server}" == 'Test2') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Test') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Test' && "${params.server}" == 'Test3') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Test') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Prod' && "${params.server}" == 'Prod1') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Prod') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Prod' && "${params.server}" == 'Prod2') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Prod') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                    if ("${params.environment}" == 'Prod' && "${params.server}" == 'Prod3') {
                            echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                            node(label: 'Prod') {
                                cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                            } 
                    }
                }
            }
        }
    }
}



