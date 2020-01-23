@Library('sast')

import com.checkmarx.sast.jenkins.CxScan
import com.checkmarx.sast.jenkins.LineOfBusiness
import com.checkmarx.sast.jenkins.ProjectTypes

pipeline {
	agent any
	stages {
		stage ('\u2776 ENV') {
			steps {
				script {
					log.info "\u2600 BUILD_URL=${env.BUILD_URL}"
					 
					def workspace = pwd()
					log.info "\u2600 workspace=${workspace}"
				}
			}
		}
		 
		stage ('\u2777 SCM') {
			steps {
				script {
					log.info 'Pulling source...'
					git 'https://github.com/randygeyer/dvna.git'
				}
			}
		}

		stage ('\u2778 SCAN') {
			steps {
				script {
					log.info 'Starting CxSAST scan...'
					def appTeam = 'GoRide'
					def appId = '12345'
					def appName = 'App1'
					def component = 'Component1'
					def branch = 'Dev'
					def environment = 'accept'
					def cx = new CxScan(this, LineOfBusiness.AppSec, ProjectTypes.WebApp, appTeam, appId, 
							appName, component, branch, environment)
					cx.addFolderExclusions('mytest,libs')
					cx.addScanComment('testing 123...')
					cx.doFullScan()
				}
			}
		}

		stage ('\u2778 OSA SCAN') {
			steps {
				script {
					log.info 'Starting CxOSA scan...'
					def appTeam = 'GoRide'
					def appId = '12345'
					def appName = 'App1'
					def component = 'Component1'
					def branch = 'Dev'
					def environment = 'accept'
					def cx = new CxScan(this, LineOfBusiness.AppSec, ProjectTypes.WebApp, appTeam, appId, 
							appName, component, branch, environment)
							
					def includeFolders = 'libs'
					def excludeFolders = ''
					cx.doOsaScan(includeFolders, excludeFolders)
				}
			}
		}
	}
}