### Notes from review with Joe 12/17/18

### Visualization

see hand-drawn paper and try to use software to make it

* Replicating tsdt app structure. Here are groups of modules and their relationships

Welcome modules:
- session viewer module
- session manage module
- session activation module

Import data modules:
- variable assignment module
- import data module
- data viewer module

Algorithm settings module:
- settings ui module

HPC module:
- HPC project settings define module
- HPC project settings viewer module
- HPC project settings execute module

Post-process module:
- import previous results
- visualization
- data table results viewer
- variable filters

### App example screenshot

* Draw arrows demonstrating the communication between the app components
    + region 1: Var selection 1 to scatterplot 1
    + region 2: Var selection 2 to scatterplot 2
    + both plots to DT module
* Emphasis on avoiding copying/pasting the code behind these modules

### Transition from road slide to example

Add a new slide(s) in between road slide to example about the principles we are teaching.  __BE AUTHORITATIVE__

Put emphasis on the principles I will illustrate in the example

Step 1: Careful Design
* What does this module do?  What is it trying to accomplish?  What ides does it emcompass? Tip: If you have trouble figuring out a function name, then you have to do some more work

Step 2: What are the inputs and outputs we need?
* Documentation plays key role here

Yes we have the boilerplate function `callModule` but that is just implementation

### Module details to highlight

* How do you determine whether you need a __static__ or a __reactive__ input?  This trips up many people
* In Shiny context: Are you passing the __present__ value or the __future__ value?
* In R functions we do this all of the time when we think carefully about the inputs and outputs, but in Shiny modules we have a third dimension to the problem __time__ (i.e. is it just the present value? or the present & future value?)
* Show why we need to use something() instead of "something" 

In plot module example code:

* dataset parameter: why is it a reactive expression and not a static value? Tell audience why

### New slide: Battle scars

* Kitchen sink approach complications
* Lack of clear documentation (building in after the fact)
* Put this after the examples and before the wrapup

### Titles for example slides

* Change titles to show what the slide conveys.
* Advice: Each slide title is like a thesis statement
* Example: __Document your Modules!__

### Module intro slide

* Change from "Functions optimized for shiny modules" to something like "Way of __breaking__ up complex apps into smaller, more understanable pieces"




### Notes from review with Joe 12/11/18

* Combine slides 8 & 9 (learning modules and roadmap for using modules in complex apps)
* Case 1 (frontend ): Pair the content down and think carefully for what my reason is to include the story. My rationale was to show that I've been through the struggles of trying to implement a custom solution for and ran in to many problems that modules does a much better job of solving
* Shiny ladder: Note that a big part of my job now is creating complex applicaitons, and I can ask the audience interactively how many have worked on large/complex applications
* Motivation:
    + We are really saying that you can't build non-trivial software without funcitons in regular R, and in the Shiny space you can't build complex Shiny apps in a robust way without modules
* Roadmap
    + Think about moving this towards beginning of presentation
    + A lot of people are accomplishing (1) successfully
    + I should emphasize that it would be surprising if those in Shiny app development are accomplishing 2 and 3 successfully
    + In the Shiny training courses offered previously, the modules portion is where most people end up getting stuck
    + Acknowledge that even Joe says that they have not done a good enough job of teaching effective use of modules
    + You have to learn some boilerplate, but once you get started it will make more sense as you go and you will get used to it
* Overall theme notes
    + This isn't so much about _best practices_ (a phrase that's been tarnished in CS space). Emphasize that modules are __essential__ to bring about software engineering best practices in Shiny app deveopment
    + Slide 2: Find a way to connect better the points (1) (about R is appealing for interactive and quick analyses), and point (2) (software engineering and shiny)
* Definition of Modules
    + Combine this with the "why should we care" slide
    + Point out that modules are to a Shiny app as functions are in R code (functions help avoid collisions in variable names)
    + Just like functions recursively break down of multiple calls, we can do a tree of modules in a recursive-like structure
    + 

### Article to-dos and feedback

* As the main content of the articles gets polished, imagine someone was squinting their eyes and only looking at various headings or other easy-to-find pieces of text. Would they be able to understand the key points without having to necessarily read the wall of text?
* For 2nd article: Illustrate why the kitchen sink approach will hurt in the long run __IN PROGRESS__
    + it can be hard to get poeple to believe that hidden state/kitchen sink is not the best approach
    + try framing the discussion around R functions: Why would anyone want to pass around some kind of environment back and forth between functions?
    + If you have a ton of inputs, no matter if you pass each of them explicitely (say a = something, b = something, etc) versus pass a list containing all of these inputs, you need to be careful to document these parameters no matter the construct you use to assemble them
    + A big reason why the kitchen-sink anti-patter is appealing is that you can read it rather easily and no other piece or other person needs to understand
    + Never want to lose sight of the contracts of our modules, just like we don't want to lose sight of the contracts of R functions
* Think about diagrams we can make to illustrate the concepts
* Another idea: If you have module a and module b, module a creates some input/UI and that is passed in to module B's ui.  Often people want to access that input from module B's server. You run into trouble because whatever module created that UI is the only one that should be able to read it correctly.  If you want to pass that to module B, you need to construct a reactive to go in to module b
* super principle: We are trying to create small pieces that are individually understandable and connect them in reeliable ways
* mmodule inputs should just be an abstraction, on server side module A's contract 

### Who is the audience?
* ~~People who haven’t used shiny~~
* People who have not used modules before
* People who have used/are using modules, but haven’t been able to connect them to each other

### What are the takeaways?
* I should use modules for larger apps
* I should create modules for reusing between apps
* There is a “right” way to do things and I should try to learn more by reading the article/looking at examples

### What are the next steps? (call-to-action)
* Go read the articles
* Use modules

### Notes from modules webinar (2016)

* Source: https://resources.rstudio.com/webinars/understandmoduleswebinar 
* Slides: https://github.com/rstudio/webinars/blob/master/19-Understanding-modules/01-Modules-Webinar.pdf 
* without modules: complex apps can be like reactive spaghetti (a lot going on, trying to isolate pieces is complicated)
* with modules: like reactive ravioli (easy to focus on pieces)
* ensure that each module is given an unique id
* pass all inputs into the module as arguments of a module function
* return all outputs as the return value of a module function
* reactive expressions are the most portable format for passing reactive information between functions
    + num() - value (reactive)
    * num - reference (not reactive)


### Outline

* Personal story about needing/using modules
    * Difficulties encountered
    *  Dead ends pursued

* Roadmap
    * Creating/using simple modules (making little islands)
    * Communication with modules (module server functions that receive input, return output)
    * Communication between sibling modules (do it only through the parent)
    * Created/used modules that can take other modules as parameters (needs better phrasing)

* Intro to modules
    * Basic example
    * Why?
        + Avoid namespace collisions
        + Organize code into easy-to-understand pieces
        + Important for scaling complexity
        + Important for “future you”
        + Important for collaborators
    * A prescribed way to combine ^ pieces (reliable composition)

* Module input/output
    *  Passing/returning reactives by name
    *  Returning multiple results using named lists
    *  Resisting the “kitchen sink approach”, i.e. passing around environments/reactiveValues (reactiveVals might be OK)
    *  Instead, think/plan/document carefully about the input/output; it’s a contract

* Combining modules
    *  Nested modules
        + Modules that call modules
    *  Sibling modules
        + Just another instance of module input/output principles
        + Use parent of the modules to coordinate between them
             + Don’t let the modules know about each other
             + Don’t let the parent know about the childrens’ implementation, only their contracts (loose coupling)
             + **Avoid relying on hidden state!**
    *  Higher order modules
        + Modules that take in other modules as parameters (usually just UI)    

* Next steps
    * Read the articles!
