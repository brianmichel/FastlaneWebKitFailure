# FastlaneWebKitFailure
A sample project using Fastlane to demonstrate the toolchain selection failure bug as reported [here](https://github.com/fastlane/fastlane/issues/5998).

# How To Test
1. Run `bundle install`
1. Run `bundle exec fastlane beta`

# Expected Result
Gym runs correctly and copies all required dylib files into the right location regardless of what toolchain the user has selected.

# Actual Result
Gym crashes with the following output when trying to copy the WebKit dylib since it is unavailable in the Xcode 8 default toolchain, but is present in the Swift 2.3 toolchain which is also included in Xcode 8.

```
bundler: failed to load command: fastlane (/Users/brianmichel/.rbenv/versions/2.2.4/bin/fastlane)
Errno::ENOENT: [!] No such file or directory @ rb_sysopen - /Applications/Xcode-beta.app/Contents/Developer//Toolchains/XcodeDefault.xctoolchain/usr/lib/swift/iphoneos/libswiftWebKit.dylib
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/2.2.0/fileutils.rb:1391:in `initialize'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/2.2.0/fileutils.rb:1391:in `open'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/2.2.0/fileutils.rb:1391:in `copy_file'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/2.2.0/fileutils.rb:485:in `copy_file'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/xcodebuild_fixes/swift_fix.rb:30:in `block (2 levels) in swift_library_fix'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/xcodebuild_fixes/swift_fix.rb:27:in `each'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/xcodebuild_fixes/swift_fix.rb:27:in `block in swift_library_fix'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/2.2.0/tmpdir.rb:88:in `mktmpdir'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/xcodebuild_fixes/swift_fix.rb:20:in `swift_library_fix'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/runner.rb:83:in `fix_package'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/runner.rb:21:in `run'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/gym-1.8.0/lib/gym/manager.rb:10:in `work'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/actions/gym.rb:22:in `run'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:190:in `block (2 levels) in execute_action'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/actions/actions_helper.rb:35:in `execute_action'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:175:in `block in execute_action'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:174:in `chdir'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:174:in `execute_action'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:100:in `trigger_action_by_name'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/fast_file.rb:140:in `method_missing'
  Fastfile:34:in `block (2 levels) in parsing_binding'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/lane.rb:33:in `call'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/lane.rb:33:in `call'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:49:in `block in execute'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:45:in `chdir'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/runner.rb:45:in `execute'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/lane_manager.rb:46:in `cruise_lane'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/command_line_handler.rb:30:in `handle'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/commands_generator.rb:49:in `block (2 levels) in run'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/commander-4.4.0/lib/commander/command.rb:178:in `call'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/commander-4.4.0/lib/commander/command.rb:178:in `call'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/commander-4.4.0/lib/commander/command.rb:153:in `run'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/commander-4.4.0/lib/commander/runner.rb:444:in `run_active_command'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane_core-0.50.3/lib/fastlane_core/ui/fastlane_runner.rb:36:in `run!'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/commander-4.4.0/lib/commander/delegates.rb:15:in `run!'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/commands_generator.rb:246:in `run'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/commands_generator.rb:20:in `start'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/lib/fastlane/cli_tools_distributor.rb:58:in `take_off'
  /Users/brianmichel/.rbenv/versions/2.2.4/lib/ruby/gems/2.2.0/gems/fastlane-1.102.0/bin/fastlane:5:in `<top (required)>'
  /Users/brianmichel/.rbenv/versions/2.2.4/bin/fastlane:23:in `load'
  /Users/brianmichel/.rbenv/versions/2.2.4/bin/fastlane:23:in `<top (required)>'
```
