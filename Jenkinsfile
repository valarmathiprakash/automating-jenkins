// Deploy the changes to Jenkins
// Additional comment

pipeline{
    agent any
    environment{
        splunk_search_head="18.170.220.94"
    }
    stages{
        stage('Deploy to Search Head'){
            steps{
                sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
                    do
                        fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
                        scp -r ${WORKSPACE}${fil} root@${splunk_search_head}:/opt/splunk/etc/apps${fil}
                    done
                '''
            }
        }
    }
}   
