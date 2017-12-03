

node {
    try {
        stage("checkout source") {
            checkout scm
        }

        // checkstyle -> dangerを実行する
        stage("code style check"){
            //結果はgithubに通知
            def CHECKSTYLE_RESULT = sh(script: "./gradlew -q checkstyle", returnStatus: true) == 0
            sh "bundle install --path vendor/bundle"
            sh "bundle exec danger"

            if(!CHECKSTYLE_RESULT){
                error "checkstyleに失敗しました"
            }
        }


        // コードのビルド
        stage("build project") {
            def BUILD_RESULT = sh(script: "./gradlew build", returnStatus: true) == 0
            if(!BUILD_RESULT){
                error "buildに失敗しました"
            }
        }

    } catch (err) {
        err_msg = "${err}"
        currentBuild.result = "FAILURE"
    } finally {
        if(currentBuild.result != "FAILURE") {
            currentBuild.result = "SUCCESS"
        }
        //notification(err_msg)
    }
}

// 実行結果のSlack通知
/*
def notification(msg) {
    def slack_channel = "#jenkins"  // jenkinsが通知するチャネル
    def slack_domain = ""           // slackのドメイン名 https://mydomain.slack.comのmydomainの部分
    def slack_token = ""            // slackのjenkinsプラグインで取得できるtoken
    def slack_color = "good"
    def slack_icon = ""
    def detail_link = "(<${env.BUILD_URL}|Open>)"  // SlackでOpenのアンカーとして表示されます
    // ビルドエラー時にメッセージの装飾を行う
    if(currentBuild.result == "FAILURE") {
        slack_color = "danger"
    }
    def slack_msg = "job ${env.JOB_NAME}[No.${env.BUILD_NUMBER}] was builded ${currentBuild.result}. ${detail_link} \n\n ${msg}"
    slackSend channel: "${slack_channel}", color: "${slack_color}", message: "${slack_msg}", teamDomain: "${slack_domain}", token: "${slack_token}"
}
*/