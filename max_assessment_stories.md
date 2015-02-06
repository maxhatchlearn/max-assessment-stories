Max’s Assessment Stories Write Up
========================================

## Section 1

### Preface

My understanding between the discussions between myself and Korei is that there will be a central rails app, in that app will be an assessment module that will hold as much of the code as possible to run our super cool customized assessment (not generate the assessments that will be builder).  90% of the App will be an ember app running on top of that that will handle the builder, cohort administration, marketplace (although there were talks of that being a separate drupal app).  There is no debate of the power of ember to run all that functionality.  The one rails database will hold everything.

The assessments will seemlessly integrate into the app, although the user will have no idea that then have actually been taken to a pure rails or possibly backbone.js route when viewing the super cool assessments  (we will even do research into doing this is emberjs as well).  The reason rails is a prefered way to do the super cool assessments is because there is a lot of hacky techniques needed to get these assessments to happen. 

For Example, I need to eval user submitted javascript on the client and run jasmine tests.  I have this running in rails no problem.  (Code academy evals user submmited javascript on the client this is the standard, doing a js sandbox on our rails app would be impractical in terms of getting the code to work and expensive computationally)


### Individual assessment/interactive demo stories

-js fiddle (my clone javascriptsandbox) html/css/javascript demos, code eval’d in client browser in iframe 

-interactive terminal session, like code academy



-assessment engine module, ruby gem, sdk