pipeline {
    agent { label 'ansible-latest' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    parameters {
        choice name: 'Project', choices: ["", "Project1", "Project2"], description: 'Please select project name'
        choice(name: 'credentialsId', choices: ["Ansible-default-key", "ansibleDefaultKeyRHEL8.4", "ansibleDefaultKeyRHEL8.8"], description: 'Please select credentialsId as per the required RHEL VERSION')
        credentials------------------------------------
        choice name: 'action', choices: ["", "restart_txn_clearlogs", "restart_webservice", "Only_clear_logs" , "Restart_Service_LogsClear"], description: 'restart tomcat & clear tomcat logs'
    }
    stages {
        stage('Run the action on component') {
            steps {
                script {
                    if (params.action == 'restart_txn_clearlogs') {
                        echo "Run the action ${params.action} on Project ${params.Project}"
                        ansiblePlaybook credentialsId: "${params.credentialsId}", extras: "-e HOST=${params.Project}", inventory: "path/inventory", disableHostKeyChecking: true, playbook: "path/OM_Tomcat2.yml"
                    } else if (params.action == 'restart_webservice') {
                        echo "Run the action ${params.action} on Project ${params.Project}"
                        ansiblePlaybook credentialsId: "${params.credentialsId}", extras: "-e HOST=${params.Project}", inventory: "path/web_inventory", disableHostKeyChecking: true, playbook: "path/web_restart.yml"
                    } else if (params.action == 'Only_clear_logs') {
                        echo "Run the action ${params.action} on Project ${params.Project}"
                        ansiblePlaybook credentialsId: "${params.credentialsId}", extras: "-e HOST=${params.Project}", inventory: "path/inventory", disableHostKeyChecking: true, playbook: "path/only_clear_logs.yml"
                    } else if (params.action == 'Restart_Service_LogsClear') {
                        echo "Run the action ${params.action} on Project ${params.Project}"
                        ansiblePlaybook credentialsId: "${params.credentialsId}", extras: "-e HOST=${params.Project}", inventory: "path/inventory", disableHostKeyChecking: true, playbook: "path/Restart_TxnOnly.yml"
                    }
                }
            }
        }
    }
}