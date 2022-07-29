# jenkins-agents-workflow
Reusable workflow for building and pushing jenkins agents docker images.

SUPPORTED TAG NAMES:
* NVM_TAG (defaults to core JDK11)
* NVM_TAG_JDK8_JDK11 (builds matrix for core JDK8 and JDK11)
* CORE_TAG (defaults to JDK11)
* CORE_TAG_JDK8_JDK11 (builds matrix for JDK8 and JDK11 defaults)

## Common Usage:

Build image with jenkins-agent-nvm default base image:
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

Build image with jenkins-agent-core default base image for JDK 11:
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

Build image with jenkins-agent-core default base images for JDK8 and JDK11:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: CORE_TAG_JDK8_JDK11
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```

## Other Usage

Build image with unsupported TAG_NAME as a part of your github workflow's build job:
```yml
    jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Build and Push Docker Image
            uses: Dwolla/jenkins-agents-workflow/.github/actions/build@main
            with:
                DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
                DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
                BASE_TAG: <my-specified-base-image-tag>
                TAG_NAME: <my-unsupported-tag-name>
                IMAGE_NAME: <my-image-name>
```

Build image with jenkins-agent-core specified base image:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: CORE_TAG
      CORE_TAG: <my-specified-core-tag>
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```

Build image with jenkins-agent-nvm specified base image:
```yml
jobs:
  build:
    uses: Dwolla/jenkins-agents-workflow/.github/workflows/build-docker-image.yml@main
    with:
      IMAGE_NAME: dwolla/jenkins-agent-*
      TAG_NAME: NVM_TAG
      NVM_TAG: <my-specified-nvm-tag>
    secrets:
      DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
      DOCKERHUB_TOKEN: ${{ secrets.DOCKERHUB_TOKEN }}
```

## Development & Contribution

To test changes, push to a new branch on jenkins-agents-workflows and modify caller-workflow to point to new branch.
* _Note: To test changes to the [composite action](./github/actions/build/action.yml) in this repository, also modify the action call in [jenkins-agent-workflow build.yml](./github/workflows/build.yml) on your branch to point to your workflow._
