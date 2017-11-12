pipeline 
{
agent any
stages
{
stage('packaging')
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
stage ('deploy_staging')
{

steps
{
build job:'deploy-to-staging'
}
}

stage ('deploy_production')
{


steps
{

timeout(time:'5',unit:'DAYS')
{
input text:'Deployment start?'
}
build job:'deploy-prod'

}
post
{
success
{

echo 'Deployment done'
}

failure
{

echo 'failed deplyment'
}

}

}

}



}
}


