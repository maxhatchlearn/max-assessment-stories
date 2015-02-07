**schema**

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
      boolean :published              ** once published always published, but can delete

    LearningPathUsers
      integer :user_id
      integer :learning_path_id
      integer :index

    LearningPathLearningModules
      integer :learning_path_id
      integer :learning_module_id
      integer :index

    LearningModules
      integer :library_id
      string :name

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




- once publish can't unpublish and no hidden draft on top of branch (word press style)