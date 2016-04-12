echo("Game of life build pipeline is starting");

node("master") {
  stage 'Code checkout'
  checkout scm

  def mvnHome = tool 'M3'

  stage 'Test'
  // run the test goals
  sh "${mvnHome}/bin/mvn -B -U clean post-integration-test"


  stage 'Build'
  // Build without running tests
  sh "${mvnHome}/bin/mvn -B -U clean install -DskipTests"
  // archive the artifacts
  step([$class: 'ArtifactArchiver', artifacts: '**/*.war', fingerprint: true])
}
