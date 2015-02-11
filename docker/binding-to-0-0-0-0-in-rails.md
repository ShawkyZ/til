# Binding to 0.0.0.0 in Rails

On OS X, [boot2docker] is an installable VM host to run Docker locally (OS X
doesn't natively support Linux Containers). In combination with [fig], it's
pretty straightforward to get a Rails application running on [Docker].

[boot2docker]: http://boot2docker.io/
[fig]: http://www.fig.sh/
[docker]: https://www.docker.com/

To access the application, you'll visit `$(boot2docker ip):3000` (or
whatever port your Rails application is running on) and things should work
fine. However, I'd recently tried setting up Docker in a Rails app that was
running WEBrick and wasn't able to access the application at all. After
updating the command to run to [Thin], the app loaded fine!

[thin]: http://code.macournoyer.com/thin/

Trevor, one of my coworkers, pointed out the binding flag in WEBrick, which
needs to be set in order for the server to accept requests from any network
interface: `rails server --binding 0.0.0.0 --port 3000`. In the current
version of Thin (v1.6.3), it looks as though it defaults to bind to 0.0.0.0
automatically.
