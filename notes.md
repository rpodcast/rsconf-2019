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