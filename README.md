# Deploy to Cloudify Github Action
This action help you to deploy your code to Cloudify.
PRs are welcome.


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
| `name`             | ***Optional***    | Name your server after deploy.
| `keypair_name`      | ***Optional***    | Your SSH Key name from Cloudify account.
| `command`           | ***Optional***    | Command for deploy, docker run.
| `flavor`           | ***Optional***    | Flavor for server(See [flavors](https://cloudify.ro/pricing/cloud-vps)).
| `image`           | ***Optional***    | Choose a image(operating system) from Cloudify, default image is `docker-ubuntu-20.04` 
| `network_id`           | ***Optional***    | For custom network, default is `public` network.

## Example usage
Example deploy for a wordpress image.

```yaml
    - uses: actions/checkout@v2
    - name: Setup Python
      uses: actions/setup-python@v1
    - name: Install Openstack Client
      uses: BSFishy/pip-action@v1
      with:
        packages: python-openstackclient
    - name: Deploy Container to Cloudify
      uses: cloudify-ro/cloudify-deploy@v1
      with: 
        credential_id: ${{ secrets.ID }}
        credential_secret: ${{ secrets.SECRET }}
        name: server-github-01
        keypair_name: test-key
        command: docker run --name wordpress-github -p 80:80 -d wordpress
```

## License
This GitHub Action and associated scripts and documentation in this project are released under the [MIT License](https://github.com/cloudify-ro/cloudify-deploy/blob/main/LICENSE).






