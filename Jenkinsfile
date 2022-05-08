properties([githubProjectProperty(displayName: '', projectUrlStr: 'https://github.com/NoyPhilosof/POC-TEST-Docker.git/')])

pipeline {
    agent { label 'ubuntu' }

    stages {
        
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'http://github.com/NoyPhilosof/POC-TEST-Docker.git'
            }
        }
        
        
        stage('Create SSH Key') {
            steps {
                catchError(message: 'Creating SSH key') {
                    script {
                        try{
                            sh '''ssh-keygen -f ~/.ssh/id_rsa -q -N ""
                            chmod 400 ~/.ssh/id_rsa'''
                        }                
                        catch (e) {
                            echo "default SSH Key exists"
                        }
                    }                
                }
            }
        }
        

        stage('Clean Old VM') {
            steps {
                catchError(message: 'Clear old VM before run') {
                    script {
                        try{
                            sh '''vagrant destroy -f
                            sleep 5'''
                        }                
                        catch (e) {
                            echo "No VM to clear"
                        }
                    }                
                }
            }
        }

        
        stage('Build VM') {
            steps {
                sh '''vagrant up
                sleep 10'''
            }
        }

        
        stage('Install docker and deploy containers') {
            steps {
                sh '''cd ansible
                ansible-playbook install-docker.yml
                ansible-playbook install-apache.yml
                ansible-playbook install-nginx.yml'''
            }
        }
        
        // stage('Example') {
        //     steps {
        //         sh 'curl 192.168.80.80:8080'

        //         script {
        //             def browsers = ['chrome', 'firefox']
        //             for (int i = 0; i < browsers.size(); ++i) {
        //                 echo "Testing the ${browsers[i]} browser"
        //             }
        //         }
        //     }


        stage('Web TEST') {
            steps {
                sh '''curl 192.168.80.80:8080
                curl 192.168.80.80:8080
                curl 192.168.80.80:8080
                curl 192.168.80.80:8080
                curl 192.168.80.80:8080
                curl 192.168.80.80:8080
                curl 192.168.80.80:8080'''
            }
        }
        

                stage('Destroy VM') {
            steps {
                sh 'vagrant destroy -f'
            }
        } 
    }
}
