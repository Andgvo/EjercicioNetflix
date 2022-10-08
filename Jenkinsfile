pipeline {
    agent any
    tools {
        maven 'M3_8_6'
    }
    stages {
        
        stage('Zuul') {
            when {
                anyOf {
                    changeset "*ZuulBase/**"
                    expression { currentBuild.previousBuild.result != "SUCCESS"}
                }
            }
            steps {
                dir("ZuulBase/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t andgvo/zuul:latest ."
                        sh 'docker stop zuul || true'
                        sh 'docker run -d --rm --name zuul -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.3.19 -p 8000:8080 andgvo/zuul:latest'
                        //sh 'docker push andgvo/zuul:latest'
                    }
                }
            }2
        }

        stage('Eureka') {
            when {
                anyOf {
                    changeset "*EurekaBase/**"
                    expression { currentBuild.previousBuild.result != "SUCCESS"}
                }
            }
            steps {
                dir("EurekaBase/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t andgvo/eureka:latest ."
                        sh 'docker stop eureka || true'
                        sh 'docker run -d --rm --name eureka -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.3.19 -p 8761:8761 andgvo/eureka:latest'
                        //sh 'docker push andgvo/eureka:latest'
                    }
                }
            }
        }
        
        stage('Ordenes') {
            when {
                anyOf {
                    changeset "*ordenes-service/**"
                    expression { currentBuild.previousBuild.result != "SUCCESS"}
                }
            }
            steps {
                dir("ordenes-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t andgvo/ordenes-service:latest ."
                        sh 'docker stop ordenes-service || true'
                        sh 'docker run -d --rm --name ordenes-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.3.19 -p 8020:8020 andgvo/ordenes-service:latest'
                        //sh 'docker push andgvo/ordenes-service:latest'
                    }
                }
            }
        }

        stage('Productos') {
            when {
                anyOf {
                    changeset "*productos-service/**"
                    expression { currentBuild.previousBuild.result != "SUCCESS"}
                }
            }
            steps {
                dir("productos-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t andgvo/productos-service:latest ."
                        sh 'docker stop productos-service || true'
                        sh 'docker run -d --rm --name productos-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.3.19 -p 8030:8030 andgvo/productos-service:latest'
                        //sh 'docker push andgvo/productos-service:latest'
                    }
                }
            }
        }

        stage('Usuarios') {
            when {
                anyOf {
                    changeset "*usuarios-service/**"
                    expression { currentBuild.previousBuild.result != "SUCCESS"}
                }
            }
            steps {
                dir("usuarios-service/"){
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker_hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh "docker build -t andgvo/usuarios-service:latest ."
                        sh 'docker stop usuarios-service || true'
                        sh 'docker run -d --rm --name usuarios-service -e SPRING_PROFILES_ACTIVE=dev -e HOST_IP_ADDRESS=192.168.3.19 -p 8010:8010 andgvo/usuarios-service:latest'
                        //sh 'docker push andgvo/usuarios-service:latest'
                    }
                }
            }
        }
    }
}