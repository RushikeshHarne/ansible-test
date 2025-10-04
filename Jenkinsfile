
pipeline {
    agent any 
    
    // Define parameters for a parameterized build
    parameters {
        string(name: 'NEW_USERNAME', defaultValue: 'test1', description: 'The username to create')
        // Use a password parameter for secure input
        password(name: 'USER_PASSWORD', defaultValue: 'root', description: 'The password for the new user') 
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clone the GitHub repository containing the playbook
                git branch: 'main', url: 'https://github.com/RushikeshHarne/ansible-test'
            }
        }
        
        stage('Run Ansible Playbook') {
            steps {
                // Execute the playbook, passing variables from the Jenkins parameters
                // Ensure your Jenkins user has SSH/sudo access to the target host
                sh """
                ansible-playbook play.yml \
                  --inventory hosts \
                  --extra-vars "new_username=${params.NEW_USERNAME} user_password=${params.USER_PASSWORD}"
                """
            }
        }
    }
}
