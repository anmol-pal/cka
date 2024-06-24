# cka

To generate yaml POD
```
k run double --image busybox --dry-run=client -o yaml > double.yaml
```

```
k api-resources
```

Worked on a Secret Management solution using AWS Secret Manager and enabling log retention with Amazon S3, all managed through Terraform scripts. This has ensured secure, automated, and consistent infrastructure provisioning and management.


Worked on creating cron jobs for repetitive db refresh tasks,created jobs which ran bash or python code under hood for automating CI/CD , Deploying K8s clusters etc