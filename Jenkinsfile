pipeline
{
    agent any

    environment{
        ACCESS_KEY=credentials('awsaccess')
        SECRET_ACC_KEY=credentials('awssecretaccess')
        VERSION_NO='1.3'

    }


    parameters {
        string defaultValue: '0.0', description: 'Enter the version number to roll back the deployment', name: 'vno'
    }
    
    stages{
        stage('Download_version'){
            steps{

                echo "checking the version"
                echo "entered version ${vno}"
                script{

                    VERSION_NO = params.vno

                }
                

                sh """
                    echo "Version number is: $VERSION_NO"
                    
                """
            }
        }

        
        stage('Rolling_Back_Deploy'){
            steps{
                
                sh """ 
                
                    cd /var/jenkins_home/workspace/version_control_job
                    mkdir -p tempDown
                    cd tempDown

                    echo 'configuring aws cred'
                    export AWS_ACCESS_KEY_ID=$ACCESS_KEY
                    export AWS_SECRET_ACCESS_KEY=$SECRET_ACC_KEY
                    export AWS_DEFAULT_REGION=us-east-1

                    echo 'Downloading the latest version of the application'
                    aws s3 cp s3://version-mangement-reactapp/${VERSION_NO}.zip .
                    unzip ${VERSION_NO}.zip


                    echo 'Deploying App to s3 bucket'
                    ls
                    aws s3 sync build/ s3://firstbucketreactapp 

                   
                """    
                
            }
            
        }
         // cd /var/jenkins_home/workspace/version_control_job
                    // rm -r tempDown
                    
        
        
    }
    
}
