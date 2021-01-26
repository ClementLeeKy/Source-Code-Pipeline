node {
      checkout scm
      
      stage ('Create Docker Registry') {
            bat 'docker run -d -p 5000:5000 --restart=always --name registry registry:2'
      }
      
      stage ('Build Docker Image') {
            def image = docker.build("docker-csv", '.') 
      }
      
      stage ('Tag and Push Docker Image') {
            bat 'docker tag docker-csv localhost:5000/docker-csv'
            bat 'docker push localhost:5000/docker-csv'
      }
      
      stage ('Pull Docker Image from Local Registry') {
            bat 'docker pull localhost:5000/docker-csv'
      }
      
      stage ('Insert Source Code as Volume into Container') {
            bat 'docker run --name source-container -d -v /c/Users/z0048yrk/Desktop/Source-Code:/root localhost:5000/docker-csv tail -f /dev/null'
            bat 'docker exec -i source-container bash'
            bat 'cd root'
            bat 'python test.py > output.csv'
       }
      
      stage ('Copy output.csv into desired directory') {
            dir("C:\\Users\\z0048yrk\\Desktop\\LTA\\new-demo") {
            bat 'docker cp source-container:/root/output.csv'
      }
   }
}
