@Library('jenkins-shared-library') _

properties([
  parameters([
    string(name: 'appVersion', defaultValue: ''),
    string(name: 'DEPLOY_TO', defaultValue: '')
  ])
])

def configMap = [
    project: 'roboshop',
    component: 'catalogue',
    appVersion: (params.appVersion),
    DEPLOY_TO: (params.DEPLOY_TO)
]
EKSDeploy(configMap)