pipeline {
  agent any
  environment {
    GH_TOKEN = credentials('jenkins-sydrawat')
  }
  stages {
    stage ('Checkout Code') {
      steps {
        cleanWs()
        checkout scm
      }
    }
    stage ('Release with SemVer') {
      tools {
        nodejs "node LTS"
      }
      steps {
          sh '''
          npm install @semantic-release/commit-analyzer
          npm install @semantic-release/release-notes-generator
          npm install @semantic-release/changelog
          npm install semantic-release-helm
          npm install @semantic-release/git
          npm install @semantic-release/github
          GITHUB_TOKEN=GH_TOKEN npx semantic-release
          '''
      }
    }
  }
  post {
    always {
      echo 'Pipeline complete'
    }
  }
}
