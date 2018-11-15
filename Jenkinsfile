properties([pipelineTriggers([githubPush()])])

node('linux') {   
	
	stage('Unit Tests') { 
		steps
		{
			git 'https://github.com/Tanya123Git/java-project.git'
			sh 'ant -f test.xml -v'   
		}
	}   
	
	stage('Build') { 
		steps
		{
			sh 'ant -f build.xml -v'   
		}
	}   
	
	stage('Deploy') {  
		steps
		{
			sh "aws s3 cp $WORKSPACE/Build/ s3://jenkins-assignment9/${env.BRANCH_NAME}/ --recursive --exclude '*' --include '*.jar'"
		}
	}
	
        stage('Report') {    
		steps
		{
			sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"  
		}
	}
}
