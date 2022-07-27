# jenkins-agents-workflow
Reusable workflow for building jenkins agents docker images

Sample calling this workflow:


Build image with jenkins-agent-nvm base image:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: NVM_TAG
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```

Build image with jenkins-agent-core base image with JDK 11:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: CORE_TAG
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```

Build image with jenkins-agent-core base image with JDK8 and JDK11:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: CORE_TAG
      BUILD_JDK_8: true
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```
