pipeline {
    agent any

    stages {
        stage('Preparation') {
            steps {
                script {
                    // Create a Session and collect the sessionId
                    def sessionId = createSession()
                    
                    // Create a Device Bundle and collect the bundleId
                    def bundleId = createDeviceBundle()
                    
                    // Define other variables
                    def appPath = 'kobiton-store:v66542'
                    def apiUrl = 'https://api-test.kobiton.com/v1/revisitPlans/start'
                    def username = 'kobitonadmin'
                    def apiKey = '05bcba8c-****-****-****-c0e3e9eb5a02'
                    
                    // Run the API trigger scriptless step
                    triggerApi(sessionId, bundleId, appPath, apiUrl, username, apiKey)
                }
            }
        }
    }
}

def createSession() {
    // Implement the logic to create a session and return the sessionId
    def sessionId = 346567
    return sessionId
}

def createDeviceBundle() {
    // Implement the logic to create a device bundle and return the bundleId
    def bundleId = 369
    return bundleId
}

def triggerApi(sessionId, bundleId, appPath, apiUrl, username, apiKey) {
    // Prepare the request payload
    def payload = '''
        {
            "exploringSessionIds": [%d],
            "appPath": "%s",
            "deviceBundleId": [%d],
            "runAllDevicesInBundle": true
        }
    '''.format(sessionId, appPath, bundleId)

    // Make the API request
    httpRequest(url: apiUrl, authentication: basicAuthentication(username: username, password: apiKey), contentType: 'APPLICATION_JSON', body: payload, httpMode: 'POST') {
        // Handle the response
        if (response.success) {
            echo "API request was successful"
        } else {
            error "API request failed with status ${response.status}"
        }
    }
}
