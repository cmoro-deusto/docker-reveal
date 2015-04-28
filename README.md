# docker-reveal
Docker container based on Ubuntu for reveal.js, including wetty and yeoman reveal generator 

## Software
[reveal.js](http://lab.hakim.se/reveal-js/#/) presentation software.

[Yeoman Generator for reveal.js](https://github.com/slara/generator-reveal)

[Wetty](https://github.com/krishnasrinivas/wetty) terminal in a browser (chrome).

## Usage
You can use it in two different ways:

- Run an existing presentation
- Develop your presentations inside the container leveraging yeoman reveal generator

### Run an existing presentation
To run an existing presentation, just mount the directoy where your preso files reside to `/home/reveal/presos`

    docker run -d -p 9000:9000 -v /path/to/preso:/home/reveal/presos dordoka/reveal

Then just got to `http://localhost:9000` on your browser to watch the slides. You can also edit the files outside the container as it's running and they will get updated, as grunt is serve-watching.

### Develop your presos using yo reveal
To develop directly your presentations, mount the parent directory where you want to persist your data to `/home/reveal/presos` and run the container interactively executing `/bin/bash`

```docker run --rm -it -p 9000:9000 -v /path/to/presos/dir:/home/reveal/presos dordoka/reveal /bin/bash```

You will drop to a command line inside `/home/reveal/presos` which will show your volume data. Within there, just create a new directory for your new slide deck and issue

```yo reveal```

to start the generator. From there, you can create new slides using

```yo reveal:slide "Slide Title"```

and edit the file generated inside the ```slides``` directory.

Check out [the reveal generator documentation](https://github.com/slara/generator-reveal) for all the options.

To start the server, just launch this from your slide deck directory

```grunt serve```

If you want to keep grunt watching the directory and autogenerating the slides on file creation or changes and leverage the reveal generator, just keep `grunt serve` running, open another terminal and execute the following

```docker exec -it <container_id> /bin/bash```

then cd to your slides deck folder and use the generator from there.

## Kudos
[Amouat reveal docker image](https://github.com/amouat/revealjs-docker)

[James Turnbull's blog post on dockerizing reveal](http://kartar.net/2014/05/presenting-with-docker/)
