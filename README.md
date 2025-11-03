# https://myarcana.github.io/url-to-text

# Convert any URL into text

Some websites don't let you copy paste from them. This is annoying for
non-developers who don't know the ins-and-outs of inspect element. It's even
annoying for developers when the site is doing it with javascript events and
other safeguards.

There already exist some URL-to-text converters public online, but I wanted to make one that:
- is 100% clientside, private and non-tracking (maybe the public proxy servers I depend on have some kind of tracking)
- supports markdown and "plaintext" output formats

Try it out at https://myarcana.github.io/url-to-text

# Technical goals

## Make a new "markdown" standard (plaintext)

This website allows you to choose markdown or plaintext output.

Plaintext output is meant to be friendly to non-technical people (e.g.
a non-computing student can just copy paste it into their flash cards), and
plaintext output is also meant to reflect the format I would send to my friends
in instant messaging apps that don't support markdown.

Generally, that's no markdown formatting at all, except for bullet lists (using
hyphens instead of stars because it's less visually busy), numbered lists, and
maybe horizontal rules.

It would be nice to specify a standard for this "rich text" "format" at some
point.

## Make a timeout queueing parallel fetcher

Some CORS proxies might take a long time to respond.

We want a response fast, but we also don't want to needlessly use all the
user's bandwidth on parallel requests, and maybe issuing multiple requests at
the same time and downloading them all will make the site even slower than
getting just one at a time would be.

I think a good solution would be setting up a "try proxy N for up to 500ms, if
no response in that time, start proxy N+1" etc. method.

