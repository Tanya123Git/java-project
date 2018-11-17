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
			import jenkins.model.*
                        jenkins = Jenkins.instance
			sh "aws s3 cp $WORKSPACE/${dist.dir}/rectangle-${env.BUILD_NUMBER}.jar s3://buckets/jenkins-assignment9/ --recursive --exclude '*' --include '*.jar'"
	}
	
        stage('Report') {    
			sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins" 
	}
}
