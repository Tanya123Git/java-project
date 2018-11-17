properties([pipelineTriggers([githubPush()])])

node('linux') {   
	
	stage('Unit Tests') { 
			git 'https://github.com/Tanya123Git/java-project.git'
			sh 'ant -f test.xml -v'   
	}   
	
	stage('Build') { 
			sh 'ant -f build.xml -v'   
	}   
	
	stage('Deploy') { 
			sh "aws s3 cp /workspace/java-pipeline/dist/ s3://jenkins-assignment9/ --recursive --exclude '*' --include '*.jar'"
	}
	
        stage('Report') { 
		withAWS(credentials:'AWS_Credential')
			{
				sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
			}
	}
}
