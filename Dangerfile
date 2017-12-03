# create a .ci_skip file to tell jenkins skip the test stage
if git.commits.first.message =~ /\[ci skip\]/ || github.pr_body =~ /\[ci skip\]/
  warn "Test stage is skipped"
  File.open(".ci_skip", "w")
end

# add JIRA's ticket url when tilte contains ticket number
# match = github.pr_title.match /\[(HATAPP-\d+)\]/
# message "JIRA Ticket: <a href='http://jira.example.com/jira/browse/#{match[1]}'>#{match[1]}</a>" if match

# a PR without any changes is invalid
fail "This PR has no changes at all" if git.modified_files.empty? && git.added_files.empty? && git.deleted_files.empty?

# check release note has changed when a release/* branch is created
# warn "Please change release note in <a href='https://ghe.example.com/HAT/HatalikeSwift/blob/#{github.branch_for_head}/fastlane/Deliverfile'>Deliverfile</a>" if github.branch_for_head.start_with?("release") &amp;&amp; !git.modified_files.include?("fastlane/Deliverfile")

# report checkstyle
github.dismiss_out_of_range_messages
checkstyle_format.base_path = Dir.pwd
checkstyle_format.report 'build/reports/checkstyle/main.xml'
checkstyle_format.report 'build/reports/checkstyle/test.xml'

# add lgtm pic
# lgtm.check_lgtm