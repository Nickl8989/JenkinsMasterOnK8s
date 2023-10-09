podTemplate(yaml: """
apiVersion: v1
kind: Pod
metadata:
    labels:
        name: jenkins
spec:
  serviceAccountName: jenkins-service-account
  containers:
  - name: jnlp
    image: jenkins/inbound-agent:latest
    command:
    - jenkins-slave
    tty: true
    env:
    - name: DOCKER_HOST
      value: 'tcp://localhost:2375'
  - name: dind-daemon
    image: 'docker:18-dind'
    command:
    - dockerd-entrypoint.sh
    tty: true
    securityContext: 
      privileged: true 
"""
) {
    node(POD_LABEL) {
      container('jnlp') {
        sh ''' 
        echo "Hello World"
        '''
      }
    }
}