node{

	stage ('Scm Checkout'){
	git credentialsId: 'github', url: 'https://github.com/anoopgawande/javahometech_my-app.git '}
	
	stage ('Mvn Package'){
	sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3/bin/mvn clean package'}

	stage ('Build Docker Image'){
	sh '/usr/bin/docker build -t agawande/my-app:$BUILD_NUMBER .'}
	
	stage ('Push Docker Image'){
	withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerpwd', usernameVariable: 'dockeruser')]) {
    sh "/usr/bin/docker login -u $dockeruser -p $dockerpwd"}
	sh '/usr/bin/docker push agawande/my-app:$BUILD_NUMBER'
	}
}
