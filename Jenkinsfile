pipeline {
   agent any
    parameters {
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }

   stages {
      stage('Hello') {
         steps {
            WORKDIR = sh (
               script: 'pwd',
               returnStdout: true
            )
            sshagent(['jenkins_id_rsa']) {
               // Using the agent resets our directory
               dir("${WORKDIR}"){
                  ansiblePlaybook(inventory: 'inventory', playbook: 'test.yml', vaultCredentialsId:'vault-password', extras: '-vvv')
               }
            }
         }

      }
   }
}
