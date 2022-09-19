<h1 align="center">Lizz compatible SMTP Server application</h1>

Lizz compatible application to add the SMTP Server application to a lizz managed Kubernetes cluster.
The SMTP Server application is simply a secret resource and a configmap resource that are added to the cluster.
These resources contain information like username, password, domain, etc... of an external STMP provider like [SendGrid](https://sendgrid.com/).

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-smtp-server \
    --path=./ \
    --destination=smtp-server \
    --set-value host=$SMTP_HOST,secure=$SMTP_SECURE,port=$SMTP_PORT,domain=$DOMAIN,smtpUsername=$SMTP_USERNAME,smtpPassword=$SMTP_PASSWORD
    --personal
```

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.


> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

