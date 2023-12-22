           pipeline {
                agent any

                stages {

                    stage('Build RPM Package') {
                        steps {
                            script {                              
                                sh ' rpmdev-setuptree'
                                sh ' wget https://github.com/Spootzz/Admin_Lab/archive/main.zip'
                                sh ' unzip main.zip'
                                sh ' mv Admin_Lab-main/rpm/calculate_files.spec ~/rpmbuild/SPECS/'
                                sh ' mv Admin_Lab-main/calculate_files.sh ~/rpmbuild/SPECS/'
                                sh ' mv main.zip ~/rpmbuild/SOURCES/'
                                sh ' rpmbuild -bs --define "dist .generic" ~/rpmbuild/SPECS/calculate_files.spec'
                                sh ' rpmbuild --rebuild ~/rpmbuild/SRPMS/calculate_files-1.0-1.generic.src.rpm'
                            }
                        }
                    }

                    stage('Install RPM Package') {
                        steps {
                            script {
                                sh ' rpm -ivh ~/rpmbuild/RPMS/noarch/calculate_files-1.0-1.el7.noarch.rpm'
                                sh ' calculate_files --check_dir=Admin_Lab-main'
                            }
                        }
                    }
                }
            }