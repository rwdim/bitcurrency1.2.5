
#!groovy

// Orig Ref From :: https://github.com/loverde/jenkinsfile-test/blob/master/Jenkinsfile
// Orig Ref From :: https://raw.githubusercontent.com/dalalv/jenkinsfiles/master/jenkinsfile-conditional-os


stage name: 'setup'
node {
    if (isUnix()) {
        echo "unix mode"
	    sh 'pwd'
        sh "ls -la"
    } else {
        echo "windows mode"
        bat "pwd"
        bat "dir"
    }
/*
    wrap([$class: 'Groovy']) {
        def script = '''
        println "\n\nSystem Properties"
        System.properties.each { k,v -> println "$k = $v" }
        println "\n\nEnvironment"
        System.getenv().each { k,v -> println "$k = $v" }
'''
    }
*/

    // Testing
    git url: 'https://github.com/loverde/jenkinsfile-test'
}

stage name: 'build'
node {
    if (isUnix()) {
      cp bitcurrency_forked/scripts/build_unix.sh ./
      chmod a+x ./build_unix.sh
      ./build_unix.sh
    } else {
        bat './gradlew.bat clean build'
    }
}

stage name: 'postbuild'
node {
    if (isUnix()) {
        sh 'ls -la'
    } else { 
        bat 'dir'
    }
}
