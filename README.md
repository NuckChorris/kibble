# Kibble
A Jekyll-inspired system for building "feed combiners" &mdash; essentially just 
websites which merge multiple sources of feed data (GitHub, Twitter, etc.) into 
one huge firehose, and then parsing that down into a website.

## Architecture
To describe the Kibble Architecture, we'll start with a step-by-step tour
through the build and deploy process.

### Triggers
Triggers are where it all starts.  These are how the Kibble daemon knows to 
retrieve, rebuild, and redeploy.  Kibble comes preloaded with
`Kibble::WebHookTrigger` and `Kibble::ManualTrigger` Triggers.  The WebHook
Trigger creates a small WEBrick server which, when you GET /, automatically 
rebuilds and redeploys.  The manual trigger is the one you generally access from
the command line; it's exposed as `kibble deploy`.

## Cans
Cans are the next step in a Kibble build process.  They represent the source
feeds of data.  They may come in gems or be placed in the `cans/` directory and 
loaded (and configured) in `config/cans.rb`.  Kibble comes preloaded with one
Can, `Kibble::Blog` &mdash; a basic markdown-powered git-fueled blogging engine,
completely (and shamelessly) ripping off the Jekyll concept.

## Bowls
Bowls are the final step, the output.  They take the time-sorted array of 
objects we got from the cans, and generate some way of displaying the results. 
Kibble's default configuration uses an ERB-based Bowl, but others are available
for JSONBuilder, HAML, etc.
