# esi-client-builder

This project automates building of my version of the client libraries
for [EVE Online](https://www.eveonline.com)'s
[ESI API](https://esi.tech.ccp.is/ui/).

ESI stands for EVE Swagger Interface; this builder uses the Swagger code
generator to build client libraries.

To perform a simple build:

```bash
$ mvn clean compile
```

For now, this only builds the source for a Ruby gem called `esi-client-bvv`,
where `bvv` is a shortened form of my character name to distinguish the gem
from other variations that might be out there.

The generated code will appear in `target/esi-client-ruby`, which is also the
name of the GitHub repository the code gets pushed to.

Once the generated code exists, there are two things you might like to do:

* Push the source to a public repository. This is not as trivial a process as
  you might hope, because of the way that the code is re-generated in full
  every time. To simplify this process, there's a `prep-ruby` script which
  does some of the repository setup. The generated repository also has a
  `git_push.sh`, but it doesn't meet my requirements (which include publishing
  as "Bora Vyvorant", rather than as his meatspace alt).

```bash
$ mvn clean
$ ./prep-ruby
$ mvn compile
$ cd target/esi-client-ruby
$ git add .
$ git commit -m "This is what is new"
$ git push --set-upstream origin master
```

* Build the gem and publish it to [RubyGems.org](https://rubygems.org):

```bash
$ gem build esi-client-bvv.gemspec
$ gem push esi-client-bvv-*.gem
```
