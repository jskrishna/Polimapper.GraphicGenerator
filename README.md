
# Constituency Infographic Project Readme

The project is split into 3 applications:
- Api
  - Handles all data access for the project
- Cartographer
  - Works against the api, allowing politics staff to manage the data
- Graphic generator
  - Works against the api, getting the data and displaying it on the map

To test the whole stack locally:
- Startup the test database (the api is configured to use a hosted test instance by default)
- Add necessary data set topologies to the database (optional)
- Add necessary node search indexes for the data set topologies (optional)
- Run the api
- Run Cartographer
- Run the map generator

All mentioned AWS services can be found in the AWS account [here](https://consumernews.signin.aws.amazon.com/console).

## Api

Handles all data access for the project. Written in C#.NET using the NancyFX framework.

Startup test database (you'll need mongodb in your PATH):
```
mongod
```

### Hosting & Deployment

The api is hosted on AWS EC2, on the same instances as the politics.co.uk and newton sites.

[This](http://www.microsoft.com/en-us/download/details.aspx?id=11342) update is required on older Windows versions to allow extensionless URLs to work correctly.

The api sits behind a CloudFront distribution *(constituency-api-cdn.politics.co.uk)* for service to the client facing map application, and is accessed directly *(constituency-api-direct.politics.co.uk)* by the internal staff facing cartographer application.

The staging deployment does not sit behind a CloudFront distribution *(constituency-api-staging.politics.co.uk)*.

## Graphic Generator

Works against the api, getting the data and displaying it on the map. Written in javascript, sass and handlebars. Requires the api running locally to test locally.

```
cd ConstituencyInfo.GraphicGenerator
```

Restore packages:

```
npm install grunt -g
npm install grunt-cli -g
npm install bower -g
gem install compass

npm install
bower install
```

Begin dev watch:

```
grunt serve
```

### Hosting & Deployment

The graphic generator is hosted on S3 *(production bucket: constituency-map.politics.co.uk / staging bucket: constituency-map-staging.politics.co.uk)* as a website, with a CloudFront distribution in front of it to allow us to use HTTPs.

Build for distribution:

```
grunt build
```

Build and deploy to S3 (staging):
```
grunt deploy:staging
```

Build and deploy to S3 (production):
```
grunt deploy:production
```

## Cartographer

Works against the api, allowing politics staff to manage the data. Written in javascript and sass using the AngularJS framework. Requires the api running locally to test locally.

```
cd ConstituencyInfo.Cartographer
```

Restore packages:

```
npm install grunt -g
npm install grunt-cli -g
npm install bower -g
gem install compass

npm install
bower install
```

Begin dev watch:

```
grunt serve
```

### Hosting & Deployment

The cartographer application is hosted on S3 *(production bucket: cartographer.politics.co.uk / staging bucket: cartographer-staging.politics.co.uk)* as a website, with a CloudFront distribution in front of it to allow us to use HTTPs.

Build for distribution:

```
grunt build
```

Build and deploy to S3 (staging):
```
grunt deploy:staging
```

Build and deploy to S3 (production):
```
grunt deploy:production
```
#   p o l i m a p p e r  
 