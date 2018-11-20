properties([pipelineTriggers([githubPush()])])

node('linux') {   
	
	stage('Unit Tests') { 
		steps {
			sh 'ant -f test.xml -v' 
			junit 'report/result.xml'
		}
	}   
	
	stage('Build') {
		steps {
			sh 'ant -f build.xml -v'   
		}
	}   
	
	stage('Deploy') { 
		steps {
			sh "aws s3 cp /workspace/java-pipeline/dist/ s3://jenkins-assignment9/ --recursive --exclude '*' --include '*.jar'"
		}
	}
	
        stage('Report') { 
		steps {
		    	withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID',
			credentialsId: 'AWS_Credential', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) 
			{
     				sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
			}
		}
				
			
	}
}
