pipeline{
    
    agent any 

    parameters{

        choice{name: 'action', choices: 'create\ndestroy\destroyekscluster'  }
    }
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
               git 'https://github.com/shriniwas-devops/demo-counter-app.git'
                }
         
            }

              stage('eks connect'){
            
            steps{
                
              sh """
                    aws eks --region example_region update-kubeconfig --name cluster_name
                    

              """
            }



      

              stage('eks deployments'){

                when{  expression { params.action == 'create'}}
            
            steps{
                
                scripts{
                    

                    def apply = false

                    try{
                        input message: please confirm the apply to intiate the deployments, ok: 'ready to apply the config'
                        apply = true

                    }
                    catch(err){
                        apply = false
                        CurrentBuild.result = 'UNSTABLE'

                    }

                    if(apply){

                        sh """
                        kubectl apply -f .
                        """;
                    }
                    
               
                }
         
            }





      






        }

    }
                
          
            
}