# Copy `terrafrom plan` directly to clipboard

At my workplace, we document for QA and historical purposes the `terraform plan` output in our issue tracking system.
Normally I spend a bunch of time highlighting sometimes extensive, multi-screen output to copy it out of my terminal.

Today, I found an easier way:


```bash
docker compose run <terraform container> bash -c "cd path/to/terraform-stuff && terraform plan -no-color" | pbcopy`
```

This will run `terraform plan` and copy it to the system clipboard. Here's a breaktown of the barts
* `docker compose run <terraform container> bash` - this will run the command inside a terraform docker container. For those that don't use docker, this can be omited
* `bash -c <command>` - this will pass and explicit command into the container. This is needed to chain together commands with `&&` inside the container
* `cd path/to/terraform-stuff` - obviously this gets us to where the right terraform code lives
* `terraform plan -no-color` - output the terrafrom plan. Strip off the color because we don't want control characters in there when pasting into the ticket system that
  won't understand them
* `| pbcody` - copy to the clipboard. This works as is on mac, but similar programs exist on linux
