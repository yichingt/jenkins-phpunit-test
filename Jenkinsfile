pipeline {
	agent any 
	stages {
		stage('Build') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y php-cli php-mbstring php-curl php-xml unzip' // Install required PHP extensions
                sh 'curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer'
                sh 'composer --version'  // Verify Composer installation
                sh 'composer install'    // Install dependencies defined in composer.json

                // List files in vendor/bin for debugging
                sh 'ls -la vendor/bin'
            }
        }
		stage('Test') {
			steps {
                	   sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
            		}
		}
	}
}
