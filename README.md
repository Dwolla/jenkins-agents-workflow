# jenkins-agents-workflow
Reusable workflow for building and pushing jenkins agents docker images.

SUPPORTED TAG NAMES:
* NVM_TAG (defaults to core JDK11)
* NVM_TAG_JDK8_JDK11 (builds amd64 for JDK8 and arm64/amd64 for JDK11)
* CORE_TAG (defaults to JDK11)
* CORE_TAG_JDK8_JDK11 (builds amd64 for JDK8 and arm64/amd64 for JDK11)

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
Also, tests run automatically for the currently supported tag names.

## Utilizing `yq` to build caller workflow images locally

With [yq](https://kislyuk.github.io/yq/) installed to build a caller image locally run the following command to retrieve the tag name:

```
curl --silent https://raw.githubusercontent.com/Dwolla/jenkins-agents-workflow/main/.github/workflows/build-docker-image.yml | yq -r .on.workflow_call.inputs.<my-core-tag>.default
```

Where `my-core-tag`&nbsp; is one of the following:
* `NVM_TAG`
* `NVM_TAG_JDK8`
* `CORE_TAG`
* `CORE_TAG_JDK8`.

Alternatively, without [yq](https://kislyuk.github.io/yq/) installed, refer to the default value(s) defined in [jenkins-agents-workflow](https://github.com/Dwolla/jenkins-agents-workflow/blob/main/.github/workflows/build-docker-image.yml):

Finally, run the following command:

`make <my-core-tag-arg-name>=<default-value-from-jenkins-agents-workflow> all`

Where `my-core-tag-arg-name` is defined in the Dockerfile and/or Makefile of the caller workflow.
