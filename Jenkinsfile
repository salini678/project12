node {

env.JAVA_HOME = tool name: 'java8', type: 'jdk'
def mvnHOME = tool name: 'maven-project', type: 'maven'
def mvnCMD = "${mvnHOME}/bin/mvn"

stage('git-clone'){

git 'https://github.com/sivaji348/addressbook.git'
}

stage('Code-Compile'){

echo "Compiling Code"
sh "$mvnCMD compile"
}
stage('Code-review'){

echo "code review"
sh "$mvnCMD pmd:pmd"
recordIssues(tools: [pmdParser(pattern: '\'**/pmd.xml')])
}

stage('Code-test'){

echo "code testing"
sh "$mvnCMD test"
}
stage('Code-coverage'){

echo "covering code"
sh "$mvnCMD cobertura:cobertura -Dcobertura.report.format=xml"
cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
}
stage('package'){

echo "package"
sh "$mvnCMD package"
}

}
