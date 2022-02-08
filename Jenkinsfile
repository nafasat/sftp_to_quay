def my_sftp_server = "10.190.0.8"
def binary_code_dir = "target/"

pipeline {
    agent {
        node { label 'quay-vm' }
    }
    stages {
        stage('get_image_from_sftp')
        {
            steps
            {
                script {
                    withCredentials([sshUserPrivateKey(credentialsId:'sftp-key', keyFileVariable: 'keyfile',usernameVariable: 'USERNAME')])
                    { 
                        sh "echo ls ${binary_code_dir} | sftp -q -oStrictHostKeyChecking=no -i ${keyfile} ${USERNAME}@${my_sftp_server} | grep \"^target\""
                    }
                }
            }
        }
    }
}
