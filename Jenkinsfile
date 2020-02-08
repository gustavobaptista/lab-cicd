pipeline {
    agent any

    stages {
        stage('Build') {
	    agent {
                docker { image 'maven:3-alpine' }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
	        archiveArtifacts 'target/*.jar'
            }
		
	stage ('Job Slack - Build') {
	    // Shell build step
		sh """ curl -X POST -H 'Content-type: application/json' --data '{
            "text": "Build customizado iniciado!",
            "attachments": [
                {
                    "text": "Deseja aprovar a GMUD?",
                    "fallback": "You are unable to choose a game",
                    "callback_id": "wopr_game",
                    "color": "#3AA3E3",
                    "attachment_type": "default",
                    "actions": [
                        {
                            "name": "ok",
                            "text": "Aprovar",
                            "type": "button",
                            "value": "ok"
                        },
                        {
                            "name": "not",
                            "text": "Reprovar",
                            "style": "danger",
                            "type": "button",
                            "value": "not",
                            "confirm": {
                                "title": "Você tem certeza?",
                                "text": "Você tem certeza?",
                                "ok_text": "Sim",
                                "dismiss_text": "Não"
                            }
                        }
                    ]
                }
            ]
        }' https://hooks.slack.com/services/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 
        """
            }
        }
    }
}
