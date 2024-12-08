pipeline {
    agent any

    stages {
        stage('Setup') {
            steps {
                sh 'mkdir -p rpm/{BUILD,RPMS,SOURCES,SPECS,SRPMS}'
                sh 'mkdir -p deb/{BUILD,DEBIAN}'
            }
        }
        stage('Build RPM') {
            steps {
                sh '''
                cp calculate-files.bash rpm/SOURCES/
                cp rpm/SPECS/calculate-files.spec rpm/SPECS/
                rpmbuild --define "_topdir $(pwd)/rpm" -ba rpm/SPECS/calculate-files.spec
                '''
            }
        }
        stage('Build DEB') {
            steps {
                sh '''
                cp calculate-files.bash deb/
                cp deb/DEBIAN/control deb/DEBIAN/
                dpkg-deb --build deb
                '''
            }
        }
    }
}
