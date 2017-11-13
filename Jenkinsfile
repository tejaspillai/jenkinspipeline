pipeline
{
agent any
parameters
{
string(name:'staging',defaultValue:'18.221.190.28',description:'staging value')
string(name:'production',defaultValue:'18.220.238.176',description:'prod server')
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

