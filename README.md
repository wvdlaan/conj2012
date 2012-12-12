conj2012
========

Notes on Clojure conj 2012



=== Rich Hickey - Keynote ===

There is a big difference between programs and systems
Programs lives in a bubble where I/O is someone else's problem
Systems live in the real world
Failure can only be addressed at the system level
Joe Armstrong's 2003 Erlang thesis:
  Making reliable distributed systems in the presence of software errors
  http://www.erlang.org/download/armstrong_thesis_2003.pdf
Rich's advice: build simple systems like e.g.;
  memcached, Zookeeper and Amazon S3



=== Everything as a value ===
Several speakers talked about values, i.e.;
  do not change the past
  do not change in place
  register everything like e.g. git or Datomic

* Stuart Halloway showed a simulation based testing approach
it was used for Datomic and will be open sourced soon
system testing = real world testing
everything is data and is stored forever;
  (1) business model ->
  (2) generated events ->
  (3) results from system under test
If you change the program
  you can check differences between result sets
  by simulating the same events
you can go back and check
  "is this problem new or did we previously miss it?"

* Rich Hickey shared ideas about codeq
git does not handle the world outside the repo
codeq adds the higher level; a bunch of repos
this is not properly defined,
  unique naming might be solved through github
git takes the SHA of a file; new SHA? then add to repo
codeq takes an additional step
A file is a directory of positons
so codeq makes a SHA for each code block in the file
new SHA? then add filename + position of code block in file to repo
if you add something to codeq you must also add a transaction record
  to document what you did
we could have a central codeq-db were you can ask questions like;
  "what libraries ever used torque?"
  "are they still using it?"
  "show me some use examples"
The next step is to get function calls in codeq

* Kovas Boguta showed how the repl-session can be a value
https://github.com/kovasb/session

* Antoni Batchelli & Hugo Duncan
thinking about moving the pallet config to datomic




=== ClojureScript ===

* Chris Granger: recent changes in LightTable
LT uses Roger Wang's node-webkit (node.js + chromium)
  https://github.com/rogerwang/node-webkit
LT will use a Component-Entity-System (CES) engine
  http://www.chris-granger.com/2012/12/11/anatomy-of-a-knockout/

* Bodil Stokke: live coding demo using node.js and webfui
catnip edi: https://github.com/bodil/catnip
node.js repl: https://github.com/bodil/cljs-noderepl

* Paul DeGrandis: using ClojureScript in the browser
learn how to use the goog library
Documentation on goog is rare: 1 book and the newsgroup
The goog libary handles browser differences really well
  but once you get to the HTML5 stuff it gets tricky
The goog library has two calling conventions
  that are different to require and call
  you need to understand this difference
Use protocols and the handy functions in shoreleave
  to avoid working directly  with the goog library
  This gives you loosely coupled code and inverted control
  https://github.com/shoreleave
If you run into troubles on the client;
  shift the work to the server
It is fine to use libraries like jQuery if you need to

* Conrad Barski demonstrated webfui;
    client side web dev framework
https://github.com/drcode/webfui
store DOM in atom as EDN
automatically keep changes in sync with the browser DOM
declare functions that have to be run when state changes

* Alan Dipert did a lighting talk on
    Functional Reactive Programming (FRP)
    in ClojureScript using Flapjax:
https://github.com/alandipert/flapjax-demo




=== Miscellaneous ===

* David Nolen added custom constraints to core.logic
he calls this 'open unification'
This helped to make the sudoku solver an order of magnitude faster
  because you can now define your custom search strategy

* Hugo Duncan gave a ritz-nrepl demo
https://github.com/pallet/ritz/tree/develop/nrepl
inspect the locals in your stacktrace (with or without locals clearing)
inspect the forms that raised compiler errors in compile time stacktraces

* a team of renowned European Clojure practitioners started lambdanext
they think about planning a training in Amsterdam second half of 2013
http://www.lambdanext.com
  Christophe Grand (enlive, Clojure Programming)
  Sam Aaron (overtone)
  Edmund Jackson (talk on Machine Learning at Clojure/conj 2012)
  Meikel Brandmeyer (vimclojure)
