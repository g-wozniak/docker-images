# Docker images

## awscli-prerender-ci
https://hub.docker.com/repository/docker/cyberforceit/awscli-prerender-ci

### About the image
Perhaps not the smallest but reliable image if you need a combo for dedicated NodeJS/ReactJS application that supports end to end testing via Puppeteer and pre-rendering mechanism with react-snap. It contains also `git`, `jq`, `curl`, `npm` and `awscli` to not annoy you with missing packages and infinitely failing pipelines.

### Our use-case
We use it to prerender React-based microsites that work on Prismic CMS.
Once the build is done, we push the content to the multiple S3 Bucket to be tested and served.

In order to make `react-snap` work we still need to manually launch the .sh script in the pipeline:

    #!/bin/bash
    mkdir ./build/rendered
    cp -avr ./build/production/* ./build/rendered
    sed -i "s/puppeteerArgs: \[\],/puppeteerArgs: \[\"--no-sandbox\", \"--disable-setuid-sandbox\"\],/" ./node_modules/react-snap/index.js

### More information
I try to review Docker images every six months to keep them up to date.