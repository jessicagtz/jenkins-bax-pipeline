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
def devServers = ["Test1", "Test2", "Test3"]
def testServers = ["Test1", "Test2", "Test3"]
def ProdServers = ["Test1", "Test2", "Test3"]

properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_MULTI_SELECT', 
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
            choiceType: 'PT_MULTI_SELECT', 
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
        description: 'Select script:'),

        string(name: 'password',
        description: 'Select script:')
    ])
])

def String[] serverGroup = "${params.environment}".split(',');

pipeline {
    agent any
    // stages in build pipeline
    stages {
        //first stage
        stage ('Parameter Validation') {
        //steps in test stage
            steps {
                echo 'The below outputs are to support any error testing.'
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

        }
        stage ('Checkout script.') {
            steps {
                node (label: 'master') {
                    git (
                    [url: 'https://github.com/tylersul/jenkins-bax.git', 
                    branch: 'master'])
                }
            }
        }
        stage ('Execute Script') {
            steps {
                script {
                for (x in serverGroup) { 
                echo "$x is being executed. \n" 
                        
                
                node (label: "$x") {
                    echo "The script being executed next is ${params.script} in the ${params.environment} on the ${params.server} server."
                        script {
                            powershell(". '.\\DeleteFiles.ps1'")
                        }
                }
                }
                        /*//cmd_exec("%SystemRoot%\\system32\\windowspowershell\\v1.0\\powershell.exe get-date > C:\\Jenkinstest.txt")
                                //script {
                                    //powershell ( 
                                    //'''
                                    //$username = "ec2amaz-389rppj\\jenkins"
                                    //$password = ConvertTo-SecureString -String ${env:password} -AsPlainText -Force
                                    //$cred = new-object -typename System.Management.Automation.PSCredential -argumentlist $username, $password
                                    //Invoke-Command -ComputerName "52.53.247.97" -credential $cred -ScriptBlock {get-date > C:\\Jenkinstest.txt}
                                    //''')
                                    //'''
                                    //$remoteUsername = "ec2amaz-389rppj\\jenkins" 
                                    //$remotePassword = "J3nk1nsUs3rn4me" 
                                    //$remoteHostname = "52.53.247.97"
 
                                    //$securePassword = ConvertTo-SecureString -AsPlainText -Force $remotePassword 
                                    //$cred = New-Object System.Management.Automation.PSCredential $remoteUsername, $securePassword
 
                                    //Invoke-Command -ComputerName $remoteHostname -Credential $cred -ScriptBlock { 
                                    //Write-Host "Hello, World (from $env:COMPUTERNAME)" 
                                    //}
                                    //'''
                                    //)
                                //} 
                    
                    //sh 'ssh -i ~/.ssh/id_rsa jenkins@52.53.247.97'
                    //sh 'dir'
                    sshPublisher(publishers: [sshPublisherDesc(configName: 'LinuxTest', 
                                                transfers: 
                                                [sshTransfer(cleanRemote: false, 
                                                excludes: '', 
                                                execCommand: 'dir', 
                                                execTimeout: 120000, 
                                                flatten: false, 
                                                makeEmptyDirs: false, 
                                                noDefaultExcludes: false, 
                                                patternSeparator: '[, ]+', 
                                                remoteDirectory: '', 
                                                remoteDirectorySDF: false, 
                                                removePrefix: '', 
                                                sourceFiles: 'hello.ps1'), 
                                                sshTransfer(cleanRemote: false, 
                                                excludes: '', 
                                                //execCommand: 'powershell "& ""C:\\users\\jenkins\\hello.ps1"""', 
                                                execCommand: 'powershell "C:\\users\\jenkins\\hello.ps1" -NAME' ${env:password},
                                                execTimeout: 120000, 
                                                flatten: false, 
                                                makeEmptyDirs: false, 
                                                noDefaultExcludes: false, 
                                                patternSeparator: '[, ]+', 
                                                remoteDirectory: '', 
                                                remoteDirectorySDF: false, 
                                                removePrefix: '', 
                                                sourceFiles: ''), 
                                                sshTransfer(cleanRemote: false, 
                                                excludes: '', 
                                                execCommand: "del ${env:password}", 
                                                execTimeout: 120000, 
                                                flatten: false, 
                                                makeEmptyDirs: false, 
                                                noDefaultExcludes: false, 
                                                patternSeparator: '[, ]+', 
                                                remoteDirectory: '', 
                                                remoteDirectorySDF: false, 
                                                removePrefix: '', 
                                                sourceFiles: '')],
                                                usePromotionTimestamp: false, 
                                                useWorkspaceInPromotion: false, 
                                                verbose: false)])
                }
            }
        }*/
    }
}



