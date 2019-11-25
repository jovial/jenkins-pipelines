pipeline {
   agent any
    parameters {
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }

   stages {
      stage('Hello') {
         environment {
            WORKDIR = sh (script: 'pwd', returnStdout: true)
         }
         steps {
            sshagent(['jenkins_id_rsa']) {
               // Using the agent resets our directory
               dir("${env.WORKDIR}") {
                  sh 'echo $WORKDIR'
               }
               sh 'pwd'
               timeout(time: 15, unit: "MINUTES") {
                  input message: 'Do you want to approve the deploy in production?', ok: 'Yes'
               }               
               ansiblePlaybook(inventory: 'inventory', playbook: 'test.yml', vaultCredentialsId:'vault-password', extras: '-vvv')
            }
         }

      }
   }
}
