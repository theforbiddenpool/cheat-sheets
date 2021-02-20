__Amazon Web Services (AWS)__ → provides on-demand cloud computing platforms and APIs to individuals, companies, and governments. We can select for the service we need and only pay for exactly what we use.

Besides Amazon, there's also Microsoft Azure and Google Cloud Platform (GCP). They try to differenciate themselves by providing different services.

## AWS Services
__EC2__ → general purpose bare metal machine to run and compute whatever you want. It's like a basic server you can run, *e.g.* Digital Ocean Linux server. We can use it to run our REST API.

__S3__ → object storage service. Each object is stored as a file with its metadata, and ID (or key). With that key, we can access the object being stored. It enables us to upload, store, and download pretty much any file or object we may want. It has a size limit of 5GB. *e.g.* store profile pictures.

__Lambda__ → run code for any type of application or backend service. We provide a function, and let it know when to run it. It has high-availability, and automatically scales. *e.g.* notify a user when they're mentioned on a message.

__CloudFront__ → speeds up distribution of our static files, similar to a CDN. Amazon delivers this content through a world wide network of data centers. Whatever server the user is closest to is the one that will deliver the files. *e.g.* HTML, CSS, and JavaScript files.

__DynamoDB__ → fast noSQL database, using the key-value storage model. Scaling is managed for us. It's known for its reliability with performance.

## Lambda Functions
The Amazon Lambda provides us with an URL, so we can send a fetch request to run the function. Under the hood, the cloud provider creates a container which contains and runs this function. If more users make a request at the same time, more containers are created to handle these incoming requests.

__Cold Start Problem__ → because the function is stored as a string in a server, when it's first run it has to be grabbed from it, and only then run. This creates a light delay in the beginning.

The function is only run when we trigger it, and when it's not running Amazon will not charge us. This is great for something that isn't running constantly.

### Serverless
Allows us to deploy lambda functions from our command line. It can be used with other cloud providers.

_Create a new template:_
```
$ npx serverless create -t aws-nodejs
```

Serverless configuration is saved in a YAML file. It's documentation can be find on [their website](https://www.serverless.com/framework/docs/).

#### Identity and Access Management (IAM)
In order to be able to deploy our lambda functions to AWS, we need to add a user to IAM, and add *Programmatic access*. Under the permission group, we can use one of the existent policies created by Amazon.

This will give us an **access key** so serveless can connect to AWS.
```
npx sls config credentials --provider aws --key <access-key-id> --secret <secret-access-key>
```
The credentials will be saved under *~/.aws/credentials*.

### Deploying the Function
All the code should be inside the `modules.exports.<name>` function. Lambda, by itself, is stateless. If we need to store state or data, we can use *DynameDB* or an *ES3 bucket*.

```
npx sls deploy
```

To test if the it's properly running, we can use:
```
npx sls invoke --function <function-name>
```
- `invoke local` → locally run the function. If it depends on other services or resources, it might not work.

# Keywords
__Infrastructure as a Service (IaaS)__ → cloud-based services, pay-as-you-go for services such as storage, networking, and virtualization. *e.g.* AWS EC2

__Platform as a Service (PaaS)__ → hardware and software tools available over the internet. It's users tend to be developers.

__Software as a Service (SaaS)__ → software that's available via a third-party over the internet, usually for a montly subscription fee.

__On-premise__ → software that's installed in the same building as our business.

[![saas vs paass vs iaas breakdown graph](https://www.bigcommerce.com/blog/wp-content/uploads/2018/10/saas-vs-paas-vs-iaas-breakdown.jpg)](https://www.bigcommerce.com/blog/saas-vs-paas-vs-iaas/#the-key-differences-between-on-premise-saas-paas-iaas "IaaS vs PaaS vs SaaS Enter the Ecommerce Vernacular – Big Commerce")

__Amazon Flowcharts__ → shows how the logic flows through someone's app.

__Serveless Architecture__ → allows us to build applications where we simple hand the cloud provider our code, and it runs it for us. The provider also makes sure that we only get charged by what we use, since it can monitor exactly what code and/or resources were used. The scaling will be taken cared for us.

# Sources
[IaaS vs PaaS vs SaaS Enter the Ecommerce Vernacular – Big Commerce](https://www.bigcommerce.com/blog/saas-vs-paas-vs-iaas/#the-key-differences-between-on-premise-saas-paas-iaas)\
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
