node('JNodes')
{
def mavenHome = tool name: "Maven Tool"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])

stage('Checkout')
{
git branch: 'main', credentialsId: '1', url: 'https://github.com/rajeshjandhyam/Java_Web_App.git'
}

stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}

stage('SonarQube Analysis')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('Jacoco Report')
{
jacoco changeBuildStatus: true, deltaBranchCoverage: '80', deltaClassCoverage: '80', deltaComplexityCoverage: '80', deltaInstructionCoverage: '80', deltaLineCoverage: '80', deltaMethodCoverage: '80', maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
}

stage('Artifact Repository')
{
sh "${mavenHome}/bin/mvn deploy"
}

stage('Deploy to tomcat')
{
deploy adapters: [tomcat9(credentialsId: '26e76d20-d22d-435c-8dea-6980e74a7dd0', path: '', url: 'http://18.204.3.181:9090/')], contextPath: null, onFailure: false, war: '**/java-web-app.war'
}

stage('Email Notification')
{
emailext body: '''Sucessfully completed the pipeline process.

Regards,
Rajesh janjam''', subject: 'Build is over', to: 'rajeshraj.techie@gmail.com'
}
}
