# Deploy to Cloudify.ro Github Action
This action help you to deploy your code to Cloudify.ro.
PRs are welcome.

[![.github/workflows/main.yml](https://github.com/cloudify-ro/cloudify-deploy/actions/workflows/main.yml/badge.svg)](https://github.com/cloudify-ro/cloudify-deploy/actions/workflows/main.yml) ![](https://img.shields.io/github/v/release/cloudify-ro/cloudify-deploy?color=blueviolet&logo=Cloudify)



## Prerequisites
The openstack client must be installed. For this we need to use `actions/setup-python@v1` and `BSFishy/pip-action@v1` to install the openstack client.
```yaml
    - name: Setup Python
        uses: actions/setup-python@v1
    - name: Install Openstack Client
        uses: BSFishy/pip-action@v1
        with:
        packages: python-openstackclient
```

## Action Inputs
| Name                  | Requirement       | Description |
|:--------------------- |:----------------- |:------------|
| `credential_id` | **Required**      | Credential id use for authentication. For generate credentials, see [here](https://help.cloudify.ro/en/article/generate-application-credentials-for-project-1wlq1za/).
| `credential_secret`         | **Required**      | Credential secret use for authentication. For generate credentials, see [here](https://help.cloudify.ro/en/article/generate-application-credentials-for-project-1wlq1za/).
| `name`             | **Required**    | Name your server.
| `keypair_name`      | **Required**    | Your SSH Key name from Cloudify.ro account.
| `command`           | **Required**    | Command for deploy, docker run.
| `flavor`           | ***Optional***    | Flavor for server(See [flavors](https://cloudify.ro/pricing/cloud-vps)).
| `image`           | ***Optional***    | Choose an image(operating system) from Cloudify.ro, default image is `docker-ubuntu-20.04` 
| `network_id`           | ***Optional***    | For custom network, default is `public` network.

## Example usage
Deploy a wordpress image.

```yaml
    - uses: actions/checkout@v2
    - name: Setup Python
      uses: actions/setup-python@v1
    - name: Install Openstack Client
      uses: BSFishy/pip-action@v1
      with:
        packages: python-openstackclient
    - name: Deploy Container to Cloudify.ro
      uses: cloudify-ro/cloudify-deploy@v1
      with: 
        credential_id: ${{ secrets.ID }}
        credential_secret: ${{ secrets.SECRET }}
        name: server-production-01
        keypair_name: user-key
        command: docker run --name wordpress-production -p 80:80 -d wordpress
```

## License
This GitHub Action and associated scripts and documentation in this project are released under the [MIT License](https://github.com/cloudify-ro/cloudify-deploy/blob/main/LICENSE).






