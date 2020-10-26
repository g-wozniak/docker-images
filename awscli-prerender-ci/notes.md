To test the application and simulate CI pipeline:

`WORKDIR /app`

`RUN git clone https://gitlab.com/cyberforce-developers/cyberforce-serverless/demo-app-web.git demo-app-web`

`WORKDIR /app/demo-app-web`

`RUN chmod +x tools/ci_hydrate.sh`

`RUN npm ci`

`RUN npm run build`