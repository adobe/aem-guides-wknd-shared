# Release Process

## Prerequisites

* You must have commit rights on this repository.
* You must have deploy rights to [Sonatype's SS Repository Hosting (OSSRH)](https://central.sonatype.org/pages/ossrh-guide.html).

## Release via GitHub Action

Release for this project is performed via GitHub Actions. The source file for the release is stored at: `.github/workflows/maven-release.yml` and dictates the workflow **Release to OSSRH**.

1. Navigate to the repo in GitHub > [Actions](https://github.com/adobe/aem-guides-wknd-shared/actions).
1. Under **Workflows** click **Release to OSSRH**
1. Choose the branch `main`. The workflow will only run against `main`.
1. Choose a release version. An odd/even version patterning is used. So for a minor release, if the current version is `1.1.0-SNAPSHOT` enter `1.2.0`.
1. Set **Dry Run** to **true** (default) and run the workflow. Ensure that the dry run release executes successfully.
1. Repeat the above steps, but set **Dry Run** to **false**. This will perform the actual release and deploy the release artifacts to a staging repository in https://oss.sonatype.org/

## Release Staging repository

Next release the artifacts in the staging repository to be deployed to Maven central.

1. Navigate to https://oss.sonatype.org/ and Log in.
1. Navigate to **Staging Repositories** and find the WKND Shared stage repo.
1. Click **Release**. Releasing the staging repo will push the artifacts to Maven Central after a small delay (4 hours for all mirrors to catch up).
1. Download the artifact `aem-guides-wknd-shared.all-X.X.X.zip`.

## Publish the Release

1. Go to https://github.com/adobe/aem-guides-wknd-shared/releases and edit the release tag and update the release text. Add compiled AEM Packages from the previous step.
1. Close any issues fixed in the release and create the next milestone.
1. Add a release announcement (and any other docs) to the documentation site.
