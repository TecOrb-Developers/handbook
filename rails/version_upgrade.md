## Upgrading Rails Project or recent version

We upgraded various old versions projects to recent Rails version. Here are some of the hardest part during the version upgrade  

### 1. Checkout used gems compatibilities in existing project with recent version.
We have to make sure to check the GitHub page of the gems we have used in the project to find out its compatibility with updated Rails version. 
[Railsbump](https://railsbump.org/) tool is very helpful to checkout gems compatibility.

### 2. Listing and updating deprecated functions, features used in the project
Major task while updating project version is to list out deprecated functions which are used in whole code base and update them as per recent version guide.

For an example when we were upgrading rails 4 project to rails 6 there is a method `update_attributes` of `ActiveRecord` class which was soft deprecated in version 5 and completely deprecated in rails 6. So we have to made changes in whole project.

[Railsdiff](https://railsdiff.org/) tool is very helpful to check the version differences. 

Suppose we are updating Rails 6 to Rails 7, here we can list all the [required changes](https://railsdiff.org/6.1.4.3/7.0.0.rc2)

### 3. Adding new features from recent version in existing project
Another challenging task was adding a new feature which was launched in recent version. We have to configure all the base configurations manually which rails does automatically in new projects.

For an example In rails 5 `ActionCable` was introduced and we had implemented action cable from base configurations to standared. We had gone though many documentations, blogs and implementations to make this worked. 

This [blog](https://samuelmullen.com/articles/introduction-to-actioncable-in-rails-5) helped us a lot during this upgrade process

### 4. Lack of project’s test coverage
We have to ensure that our application should works after upgrading. And this is possible only if we have good test coverage before we start the process. 

If we don't have automated tests that test the features of our application, we will need to spend time manually to test all the parts that have changed.

So we should have at least 80% test coverage unless we have a dedicated QA team.

### 5. Best way to update existing project to Rails 7
Before upgrade to Rails 7 at least we have to gone through Hotwire which includes Turbo and Stimulus because 
- Webpack and Node are not required
- UJS and Turbolinks is now replaced Stimulus and Turbo.

#### Helpful links
- [How to Prepare Your Rails App for an Upgrade](https://www.fastruby.io/blog/rails/upgrade/prepare-for-rails-upgrade.html)
- [Next Rails - toolkit to upgrade your next Rails application](https://github.com/fastruby/next_rails)
- [Upgrade Rails 6 to Rails 7](https://www.fastruby.io/blog/rails/upgrades/upgrade-rails-6-1-to-7-0.html)
- [rails:update](https://thomasleecopeland.com/2015/08/06/running-rails-update.html)
- [Railsdiff](https://railsdiff.org/)
- [Railsbump](https://railsbump.org/) 
