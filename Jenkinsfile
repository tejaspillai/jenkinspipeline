pipeline
{
agent any
stages{

stage('package')
{
steps{

sh 'mvn clean package'
}
post
{
success
{

archiveArtifact artifacts:'**/target/*.war'

}
}
}
stage('deploy')
{

steps{

build job:'deploy-to-staging'
}
post
{
success
{
echo 'success'
}
}
}
}
}
