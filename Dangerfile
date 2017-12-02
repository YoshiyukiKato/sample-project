# create a .ci_skip file to tell jenkins skip the test stage
if git.commits.first.message =~ /\[ci skip\]/ || github.pr_body =~ /\[ci skip\]/
  warn "Test stage is skipped"
  File.open(".ci_skip", "w")
end

# add JIRA's ticket url when tilte contains ticket number
# match = github.pr_title.match /\[(HATAPP-\d+)\]/
# message "JIRA Ticket: <a href='http://jira.example.com/jira/browse/#{match[1]}'>#{match[1]}</a>" if match

# a PR without any changes is invalid
fail "This PR has no changes at all" if git.modified_files.empty? &amp;&amp; git.added_files.empty? &amp;&amp; git.deleted_files.empty?

# check release note has changed when a release/* branch is created
# warn "Please change release note in <a href='https://ghe.example.com/HAT/HatalikeSwift/blob/#{github.branch_for_head}/fastlane/Deliverfile'>Deliverfile</a>" if github.branch_for_head.start_with?("release") &amp;&amp; !git.modified_files.include?("fastlane/Deliverfile")

# run swiftlint
# github.dismiss_out_of_range_messages
# swiftlint.config_file = '.swiftlint.yml'
# swiftlint.lint_files inline_mode: true

# run checkstyle
# TODO: ここの設定を書く
github.dismiss_out_of_range_messages
checkstyle_format.base_path = Dir.pwd
checkstyle_format.report 'app/build/reports/checkstyle/checkstyle.xml' #ここのパスは変える必要あり


# add lgtm pic
lgtm.check_lgtm