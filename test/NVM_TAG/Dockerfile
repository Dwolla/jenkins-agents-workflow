ARG NVM_TAG

FROM dwolla/jenkins-agent-nvm:$NVM_TAG

USER root
RUN chown -R jenkins ${JENKINS_HOME}

USER jenkins