pipeline {
   agent any
    parameters {
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }

   stages {
      stage('Hello') {
         WORKDIR = sh (
            script: 'pwd',
            returnStdout: true
         )
         steps {
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
