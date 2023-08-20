pipeline {
   agent {
        node {
               label 'Jenkins'
        }
    }
   parameters {
        gitParameter(branchFilter: '.*',
        defaultValue: 'master',
        name: 'BRANCH',
        description: 'Select Branch',
        quickFilterEnabled: true,
        selectedValue: 'NONE',
        sortMode: 'DESCENDING_SMART',
        tagFilter: '.*',
        type: 'PT_BRANCH_TAG',
        useRepository: 'Jenkins_Sample_Pipeline_Declarative.git')
        string(name: 'INPUT_PARAM', defaultValue: 'NULL', description: 'Enter the Input value')
        text(name: 'TEXT_BOX', defaultValue: 'NULL', description: 'Enter the text value')
        choice(name: 'CHOICE_PARAM', choices: ['One', 'Two', 'Three'], description: 'Choose from Dropdown')
        booleanParam(name: "CHECK_BOX", defaultValue: false)
    }
     stages{
    stage('Cleanup Job Workspace before job starts') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace before Jobs starts"
                """
            }
        }
    stage('GIT Checkout'){
    steps {
             sh """
                echo "Checking out code from Git Repo"
	        """
              checkout([$class: 'GitSCM', branches: [[name: "${params.BRANCH}"]], userRemoteConfigs: [[credentialsId: 'JENKINS_GITHUB_TOKEN', url: 'https://github.com/navachaitanyak/Jenkins_Sample_Pipeline_Declarative.git']]])             
           }
    }
    stage('This stage will execute when checkbox is set to true'){
        
        when{ expression { params.CHECK_BOX } }
        steps {
            sh """
            echo "echo 1"
	    echo "${params.INPUT_PARAM}"
            """
        }
	}
    stage('Input Validation'){
        steps {
            sh """
                echo "${params.INPUT_PARAM}"
	        """
        }
    }
    }
	post {
		success {
			echo 'Sending Email on Pipeline Success'
		}
		failure {
			echo 'Sending Email on Pipeline Failure'
		}
	}
}
