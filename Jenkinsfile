pipeline {
    agent any

tools {
    nodejs "node"
  }
parameters {
    string(name: 'container_name', defaultValue: 'appmonte_test', description: 'Nombre del contenedor de docker.')
    string(name: 'image_name', defaultValue: 'montetest_img', description: 'Nombre de la imagene docker.')
    string(name: 'tag_image', defaultValue: '0.0.5', description: 'Tag de la imagen de la pagina.')
    string(name: 'user_docker', defaultValue: 'ocampoomar082', description: 'usuario docker')
 
  }

 stages {
    stage('GitClone') {
      steps {
	    deleteDir()
        git branch: 'main', credentialsId: 'github_1', url: 'https://github.com/ocampoomar082-png/piedadJava.git'
	
        }
      }//Fin Git Clone  
	  
	stage('NPMInstall') {
      steps {
	
		 dir('frontend') {
          bat 'npm install'
        }
        }
      }//Fin install npm
    
    
    stage('TestUnitarios') {
      steps {
        dir('frontend') {
          bat 'npm run test'
        }
      }
    }//Fin Test Unitarios
	
	stage('Build') {
      steps {
        dir('frontend') {
         bat 'npm run build'
       }
         
     }
	 
   }//Fin Build
   
    stage('Contenerizado') {
            steps {
                script {
                    FAILED_STAGE = env.STAGE_NAME
                    echo "Stage Contenerizado Inicio"
                    try {
                        sshPublisher(
                            continueOnError: false,
                            failOnError: true,
                            publishers: [
                                sshPublisherDesc(
                                    configName: 'server-docker', // Servidor configurado en Jenkins
                                    transfers: [
                                        sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execTimeout: 120000,
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: '',
                                            remoteDirectorySDF: false,
                                            removePrefix: '',
                                            sourceFiles: 'frontend/dist/frontend/,frontend/nginx.conf,Dockerfile',
                                            execCommand: """
                                                echo "Eliminando directorio anterior..."
                                                (rm /home/vboxuser/monteimages/${container_name} || true)
                                                mkdir -p /home/vboxuser/monteimages/${container_name}
                                                echo "Directorio preparado correctamente."
                                            """
                                        ),
                                            sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execTimeout: 120000,
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: "${container_name}",
                                            remoteDirectorySDF: false,
                                            removePrefix: '',
                                            sourceFiles: 'frontend/dist/frontend/,frontend/nginx.conf,frontend/dockerfile',
                                             execCommand: """
                                                cp -R /home/vboxuser/monteimages/${container_name}/frontend/dockerfile /home/vboxuser/monteimages/${container_name} && \\
                                                cd /home/vboxuser/monteimages/${container_name}/frontend/ && \\
                                                docker build -t ${user_docker}/${image_name}:${tag_image}  .
                                                docker push ${user_docker}/${image_name}:${tag_image}
                                                docker save ${user_docker}/${image_name}:${tag_image} -o ${image_name}_${tag_image}.tar
                                            """
                                        )
                                    ],
                                    usePromotionTimestamp: false,
                                    useWorkspaceInPromotion: false,
                                    verbose: true
                                )
                            ]
                        ) // sshpublish
                    } catch (err) {
                        echo err.getMessage()
                        String logData = currentBuild.rawBuild.getLog(50) // ojo: X no estaba definido
                        error "Pipeline aborted: No se concluya la construccion del microservicio"
                    }
                }
            }
        } // Fin Contenerizado
    
	stage('DeployDockerHub') {
            steps {
                script {
                    FAILED_STAGE = env.STAGE_NAME
                    echo "Stage Contenerizado Inicio"
                    try {
                        sshPublisher(
                            continueOnError: false,
                            failOnError: true,
                            publishers: [
                                sshPublisherDesc(
                                    configName: 'server-docker', // Servidor configurado en Jenkins
                                    transfers: [
                                       
                                            sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execTimeout: 120000,
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: "${container_name}",
                                            remoteDirectorySDF: false,
                                            removePrefix: '',
                                            sourceFiles: 'frontend/dist/frontend/,frontend/nginx.conf,frontend/dockerfile',
                                             execCommand: """
                                                
                                                docker push ${user_docker}/${image_name}:${tag_image}
                                               
                                            """
                                        )
                                    ],
                                    usePromotionTimestamp: false,
                                    useWorkspaceInPromotion: false,
                                    verbose: true
                                )
                            ]
                        ) // sshpublish
                    } catch (err) {
                        echo err.getMessage()
                        String logData = currentBuild.rawBuild.getLog(50) // ojo: X no estaba definido
                        error "Pipeline aborted: No se concluye la construccion del microservicio"
                    }
                }
            }
        } // Fin Push Docker
    
	stage('FinPipeline') {
      steps {
       echo 'Pipeline Terminado con'
         
     }
	 
   }//Fin Build
    
  } 
  }
 

