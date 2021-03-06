Max’s Super Cool Assessment Stories Write Up
========================================

## Section 1

### Preface

Hold on to your seats, because there is no more assessment model!!!! But we do have Page and Section models!

My understanding between the discussions between myself and Korei is that there will be a central rails app, in that app will be an assessment module that will hold as much of the code as possible to run our super cool customized assessment (not generate the assessments that will be builder).  90% of the App will be an ember/angular/backbone app running on top that will handle the builder, cohort administration, marketplace (although there were talks of that being a separate drupal app).  The one rails database will hold everything (not considering optimization).

The "assessments" (really the path view now) will seemlessly integrate into the app, although the user will have no idea that then have actually been taken to a pure rails or possibly backbone.js route when viewing the super cool assessments.  The reason rails is a prefered way to do the super cool assessments is because there is a lot of hacky techniques needed to get these assessments to happen. 

For Example, I need to inject and eval user submitted javascript into the template on the client and run jasmine tests.  I have this running in rails no problem.  (Code academy evals user submmited javascript on the client this is the standard, doing a js sandbox on our rails backend would be impractical in terms of getting the code to work and expensive computationally).  We would have to change the default templating engine on ember to eval js code and it would just kill the whole beauty of an ember template, or make a complicated helper.

The super cool assessments can either be built onto the main rails app or be a separate rails app that connects to the database.

### Overall Assessment structure

We want the best of everything!

We want a ruby monk (and also JS and Scala monk!) style markdown interspersed with cool rspec driven examples and challenges.

Ruby Monk style assessments/problems will need to have markdown that preceeds and follows the assessment.  

At this point I am assuming that the assessment will be json based, and refer to the markdown, ruby, javascript files in a folder or same folder.

![](ruby_monk01.png)

**Lets figure what what that is going to look like**

Following the Ruby Monk model we have a Section called "Introduction To Ruby Objects" that consists of 3 pages 

[check it out for yourself (might have to login)](https://rubymonk.com/learning/books/1-ruby-primer)

![](ruby_monk02.png)

I am feeling that the Path is named Ruby Primer, with a list of authors, and a description


Then we have modules like "Introduction To Ruby Objects", "Introduction to Strings", that only have names.  (Note: in my versioning schema, modules must be connected to paths by a join table because the same version of module might belong to many versions of a path, but to get these super cool assessments working, we really might just want to brute force version things using local git repos in hatchdown/json format)

"Introduction to Objects", "More Objects and Methods" are each names of Assessments in the "Introduction To Ruby Objects" module.

That was straight forward; now it gets kind of tricky.  It seems that the assessment parts will have to be grouped into sections.  (Note generally I dont give my join tables library_ids, I have decided to only give my Paths, modules, videos, marks, assessments library_ids)

We will need answer models and if all the answers for assessment problems that aren't example are answered then an assessment gets a checkmark.  And of course we will save the problem answers

***************
**New schema**

    Users
      string :github_login
      integer :github_id
      string :session_token
      string :github_access_token

    Libraries
      integer :user_id
      string :name

    LearningPaths                     **one picture is associated with learning path
      integer :library_id
      string :name
      string :description
      string :skill_level             ** beginner, intermediate, expert

    LearningPathUsers
      integer :user_id
      integer :learning_path_id
      integer :index

    LearningModules
      integer :library_id
      integer :learning_path_id
      string :name
      integer :index

    Pages
      integer :learning_module_id
      integer :library_id
      string :name
      integer :index

    Sections
      integer :page_id
      string :name
      integer :index

    SectionAssets
      integer :section_id
      references :asset, polymorphic: true
      integer :index

    Terminal
      integer :page_id
      string :name
      text :markdown
      text :instructions            ** in markdown
      text :src
      text :hint                    ** in markdown might be null
      integer :index

    Fiddles
      text :html
      text :css
      text :javascript

    Marks
      text :src

    Videos
      text :url

    Challenges
      string :language
      boolean :example                **if true then src = solution and solution null
      text :src
      text :solution
      text :spec

    ChallengeAnswers
      integer :challenge_id
      integer :user_id
      text :src
      boolean :success

    SectionCompletes
      integer :user_id
      integer :section_id
      boolean :complete

    Project
      string :name
      string :language
      text :spec
      *** need to attach a zip file with paperclip



** a section might have a name then markdown then challenge then markdown then a fiddle

** a section might have a name then markdown then a project

** a page might have a bunch of terminal sessions in it, in which case it will not actually be one page, but a next button will appear because the terminal session takes up the whole page

** if a page only has video and marks then a "got it" button appears to create the sectioncomplete instance

****************

Versioning scheme is like koreis and hybrid of mine

when you create a learning path there is always a commit join table (no longer polymorphic), that has the unpublished version



[new unpublished learning path]

[published learning path]----[Commit]---[unpublished learning path]


- Actually i don't like that versioning scheme

I like everything to be versioned the way i had it with my original versioning scheme
  Don't want to be sending out false notification that something you forced got 
  that would require bringing back all joining to be done with join tables


*************


But then we might want to go to a live terminal session or jsfiddle type demo.

The all in one page thinkster style will quickly break down.

Live terminal session should be all in one page with a next button.

js fiddle type demo should be preceeded/surrounded with markdown in an assessment section, but really isn't an assessment per say, so the definition of assessment is kind of breaking down.

Question: can I grade a css/html/javascript thing?

I have to think more about how i want the flow of a js fiddle type demo to flow into a ruby monk style thing.  Also need css/paper prototypes for each page.




This will most likely be accomplished with the following Schema




### Individual assessment/interactive demo stories

- standard problem types, multiple choice, checkbox (check all that apply), text input (write an essay, or answer a math question, etc)

- js fiddle (my clone javascriptsandbox) html/css/javascript demos, code eval’d in client browser in iframe 

- interactive terminal session, like code academy or dataquest.io

- Project zips you download that are almost finished projects, that are too complicated to do in browser (full on rails app with sqlite db, or multi file javascript app), you finish the specs and upload it and we rerun the specs and record your score.  Within this topic there will be practice assessments and full on timed assessments.

- simple coding exercises/ challenges.  This can be 


- assessment engine module, sdk, open source ruby gem that other people can bring into their app that will make assessments come to life, and down the road send back analytics to us




- possibility: edx style write your own javascript to make a problem





- Versioning brainstorm:  could do brute force versioning of the module to a local repo? that would be a lot of repos, makes more sense to just have the whole path be a repo that when things change.  

  - Thats good in someways, just leave versioning to local gits


- assessment spec for a spec, download project and complete the spec spec, then upload and well test your app



