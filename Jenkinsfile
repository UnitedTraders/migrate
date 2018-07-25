@Library('jenkins-helpers') _

node {
    try {

        checkoutSources()

        git_branch = env.BRANCH_NAME
        if (git_branch == "master") {
            tag = "latest"
        } else {
            tag = git_branch
        }

        stage("Build")
        sh """
            docker build -t registry.auroraplatform.com/clickhouse-migrate-main:${tag} .
        """

        stage("Push Artifact")
        sh """
            docker push registry.auroraplatform.com/clickhouse-migrate-main:${tag}
        """

    } catch (e) {

        reportFailedBuild(e)

    }
}
