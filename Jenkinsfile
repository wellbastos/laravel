node('PHP'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --no-scripts --prefer-dist --no-dev --ignore-platform-reqs'
    }
    
    stage('config') {
        parallel(
            'config cache': {
              echo 'tarefa paralela '
            }
        )
    }
    stage('Docker Build') {
        sh 'docker build -t wellbastos/laravel:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push wellbastos/laravel:$BUILD_NUMBER'
    }
}
