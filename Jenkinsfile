// // Declarative Pipeline
// pipeline {
//     agent none
//     stages {
//         stage('Build') {
//             agent {
//                 docker {
//                     image 'python:2-alpine'
//                     args '-v /var/run/docker.sock:/var/run/docker.sock'
//                 }
//             }
//             steps {
//                 sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             }
//         }
//         stage('Test') {
//             agent {
//                 docker {
//                     image 'qnib/pytest'
//                     args '-v /var/run/docker.sock:/var/run/docker.sock'
//                 }
//             }
//             steps {
//                 sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//             }
//             post {
//                 always {
//                     junit 'test-reports/results.xml'
//                 }
//             }
//         }
//     }
// }

// Scripted Pipeline
node {
    stage('Build') {
        docker.image('python:2-alpine').inside('-v /var/run/docker.sock:/var/run/docker.sock') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    stage('Test') {
        docker.image('qnib/pytest').inside('-v /var/run/docker.sock:/var/run/docker.sock') {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            junit 'test-reports/results.xml'
        }
    }
}
