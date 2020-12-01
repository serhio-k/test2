pipeline {
    agent none

    environment {
        BRANCH='dev'
        REPO1='https://github.com/serhio-k/sklbx.git'
        REPO2='https://github.com/serhio-k/zabbix.git'
        REPO3='https://github.com/serhio-k/TDM.git'
        BUILD_SCRIPTS1='skillbox'
        BUILD_SCRIPTS2='zabbix'
        BUILD_SCRIPTS3='tdm'
        BUILD_HOME='/var/lib/jenkins/workspace'
        }

    stages {

        stage('Checkout_first') {
            steps {
                checkout([
        $class: 'GitSCM', 
        branches: [[name: '*/master']], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [[$class: 'CleanCheckout']], 
        submoduleCfg: [], 
        userRemoteConfigs: [[credentialsId: 'github_access_token', url: env.REPO1]]
    ])
            }
        }

        stage('Checkout_second') {
            steps {
                checkout([   $class: 'GitSCM',
         branches: [[name: env.BRANCH]],
         doGenerateSubmoduleConfigurations: false,
         extensions: [[$class: 'CleanBeforeCheckout'],
                      [$class: 'SubmoduleOption',
                       disableSubmodules: false,
                       parentCredentials: true,
                       recursiveSubmodules: true,
                       reference: '',
                       trackingSubmodules: false],
                      [$class: 'RelativeTargetDirectory',
                       relativeTargetDir: 'zabbix/']],
         submoduleCfg: [],
         userRemoteConfigs: [[credentialsId: github_access_token, url: env.REPO2]]
       ])
            }
        }

        stage('Checkout_third') {
            steps {
                checkout([   $class: 'GitSCM',
         branches: [[name: env.BRANCH]],
         doGenerateSubmoduleConfigurations: false,
         extensions: [[$class: 'CleanBeforeCheckout'],
                      [$class: 'SubmoduleOption',
                       disableSubmodules: false,
                       parentCredentials: true,
                       recursiveSubmodules: true,
                       reference: '',
                       trackingSubmodules: false],
                      [$class: 'RelativeTargetDirectory',
                       relativeTargetDir: 'tdm/']],
         submoduleCfg: [],
         userRemoteConfigs: [[credentialsId: github_access_token, url: env.REPO3]]
       ])
            }
        }
        stage('Check') {
            steps {
                sh "ls -laih"
            }
        }
    }
}
