# RootPrompt Demo App (v1 & v2)

This example demonstrates how to build two distinct Docker images that serve different HTML content.  
You’ll see a visible change when curling the service after switching versions.


## Create Dockerfiles and HTML

```bash
cat <<EOF > Dockerfile-v1
FROM nginx:1.26.0
COPY index.html /usr/share/nginx/html/index.html
EOF

cat <<EOF > index-v1.html
<!DOCTYPE html>
<html>
<head>
  <title>RootPrompt App - V1</title>
</head>
<body>
  <h1>Hello from RootPrompt App v1 </h1>
  <p>This is the first release of our demo app.</p>
</body>
</html>
EOF

cat <<EOF > Dockerfile-v2
FROM nginx:1.26.0
COPY index.html /usr/share/nginx/html/index.html
EOF

cat <<EOF > index-v2.html
<!DOCTYPE html>
<html>
<head>
  <title>RootPrompt App - V2</title>
</head>
<body>
  <h1>Hello from RootPrompt App v2 🎉</h1>
  <p>This is the upgraded release with new content.</p>
</body>
</html>
EOF
```

## Build Images

```bash
docker build -f Dockerfile-v1 -t rootpromptnext/app:v1 .
docker build -f Dockerfile-v2 -t rootpromptnext/app:v2 .
```

## Run & Test Locally

```bash
docker run -d -p 30120:80 rootpromptnext/app:v1
curl http://localhost:30120
# → Shows "Hello from RootPrompt App v1"

docker run -d -p 30121:80 rootpromptnext/app:v2
curl http://localhost:30121
# → Shows "Hello from RootPrompt App v2"
```

## Push to Docker Hub

```bash
docker login -u rootpromptnext

docker push rootpromptnext/app:v1
docker push rootpromptnext/app:v2
```


## Outcome
- `rootpromptnext/app:v1` → serves Version 1 HTML  
- `rootpromptnext/app:v2` → serves Version 2 HTML  
- Updating your Kubernetes Deployment from `v1` to `v2` will visibly change the curl output.
```

