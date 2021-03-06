desc "Test if SASS files are compiling"
task test: ["test:lint", "test:install_bower_deps", "test:compile", "test:cleanup"]

desc "SASS test tasks"
namespace :test do

  desc "Lint SASS files"
  task :lint do

    `gem install scss-lint`
    result = `scss-lint ./`

    if result.include? "[E]"
      raise "Linting Sass files failed"
    else
      puts "Sass files linted successfully"
    end
  end

  desc "Install Bower dependencies"
  task :install_bower_deps do

    # https://github.com/bower/bower/pull/1163
    `npm install`
    `npm install -g bower`
    result  = `bower install westfieldlabs/scally --config.interactive=false`

    puts "Bower dependencies installed successfully"

  end

  desc "Compile SASS files"
  task :compile do

    result = `sass style-test.scss test.css`

    raise result unless $?.to_i == 0

    raise "Compiling Sass files failed" unless File.exists?('test.css')

    puts "Sass files compiled successfully"

  end

  desc "Clean up CSS files"
  task :cleanup do

    Dir["*.css"].each do |css|
      `rm #{css}`
      `rm #{css}.map` if File.file?("#{css}.map")
    end

    puts "CSS files cleaned up and Bower dependencies removed successfully"
  end

end
