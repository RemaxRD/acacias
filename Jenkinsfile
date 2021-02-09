def TIMESTAMP = Calendar.getInstance().getTime().format('YYYYMMdd-hhmm')

pipeline {
  agent {
    label "master"
  }

  environment {
    AGENT_NAME  = "acacias"
    AGENT_URL   = "https://hopeful-northcutt-9fee52.netlify.app/"
  }

  stages {


    stage("Validation") {
      steps {
        timeout (time: 15, unit: 'MINUTES') {
          input message: 'Are you sure you want to deploy the agent? (Click "Proceed" to continue...)'
        }
      }
    }


    stage("Initialize") {
      steps {
        sh(
          label: "Run agent deploy",
          script: """
            cd /srv/deployment/remax/stage
            ansible-playbook agent.yml --extra-vars "agent_name=${AGENT_NAME} agent_url=${AGENT_URL}"
          """
        )
      }
    }
  }
}
