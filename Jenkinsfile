pipeline {
   agent any
    parameters {
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }

   stages {
      stage('Hello') {
         steps {
            ansiblePlaybook(credentialsId: 'jenkins_id_rsa', inventory: 'inventory', playbook: 'test.yml', vaultCredentialsId:'vault-password', extras: '-vvv')
         }

      }
   }
}
