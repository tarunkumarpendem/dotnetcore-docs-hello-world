pipeline
{
    agent {
        label '.net6'
    }
    parameters{
        choice(name: 'Branch_to_Build', choices: ['master', 'dotnet'], description: 'Branch to be selected')
    }
    post{
        always{
            echo 'build completed'
        }
        failure
        {
            echo 'build failed'
        }
        success{
            echo 'build success'
        }
    }
    stages{
        stage('clone'){
            steps{
                git url: 'https://github.com/tarunkumarpendem/dotnetcore-docs-hello-world.git',
                    branch: "${params.Branch_to_Build}"
            }
        }
        stage('script'){
            steps{
                script{
                sh """dotnet build dotnetcoresample.csproj
                      dotnet publish dotnetcoresample.csproj
                      zip -r dotnetcore-docs-hello-world-1.0.0.zip /home/ubuntu/dotnetcore-docs-hello-world/bin/Debug/net6.0/publish
"""
               }
            }
        }
        stage('Archiving_Artifcats'){
            steps{
                archiveArtifacts artifacts: '**/*.zip'
            }
        }
    }
}