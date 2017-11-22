pipeline
{
agent any
parameters
{
string(name:'staging',defaultValue:'18.216.64.114',description:'staging value')
string(name:'production',defaultValue:'52.15.235.78',description:'prod server')
}
triggers
{

pollSCM	('* * * * *')
}
stages
{
stage('package')
{
steps
{
sh 'mvn clean package'
}
post
{
success
{
archiveArtifacts artifacts:'**/target/*.war'
}

}


}
stage('deploy')
{
parallel
{
stage('deploy_stage')
{
steps{

sh "chmod 777 **/target/*.war"

sh "scp -i /root/tomcat_demo.pem **/target/*.war ec2-user@${params.staging}:/var/lib/tomcat7/webapps"

}

}
stage('deploy_prod')
{
steps{
sh "chmod 777 **/target/*.war"

sh "scp -i /root/tomcat_demo.pem **/target/*.war ec2-user@${params.production}:/var/lib/tomcat7/webapps"

}

}



}
}
}

}

