ARG CORE_TAG

FROM dwolla/jenkins-agent-core:$CORE_TAG

USER root
RUN chown -R jenkins ${JENKINS_HOME}

USER jenkins