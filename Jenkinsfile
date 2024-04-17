pipeline {
    agent any
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
 
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
 
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
 
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
 
        string(name: 'USERNAME', defaultValue: 'USERNAME', description: 'Enter a username')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

        string(name: 'STAGE', defaultValue: 'PRD', description: 'Enter a stage')
    }
    stages {
        stage('Example') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Username: ${params.USERNAME}"

                echo "Password: ${params.PASSWORD}"

                echo "Stage: ${params.STAGE}"
            }
        }
    }
}