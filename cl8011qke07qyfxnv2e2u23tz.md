# Automate Your Python Package Release w/ GitHub Actions

You're probably developing your Python package on GitHub and you use `sdist` and `twine` to make a new build and upload it to pypi.org. Then, you create a new release in the package repository. What if you could automate this process and your new package gets uploaded to PyPI automatically once you create a new release on GitHub?! That's what we're going to talk about today.

### Grant A New PyPI Access Token
At first glance, you need to either create a new account or log into your PyPI account on pypi.org/account/login.

Navigate to the "Account Settings" and find the "API tokens" section and "Add API token".

![Screenshot_2022-09-11_13-46-39.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662888102666/MBdTUoz-N9.png align="center")

As you can see, I already have two tokens generated for my projects. Once you hit the "Add API token", fill out the following form.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662888233723/1ZW70nxnG.png align="center")

> Warning: You better choose different tokens for different projects. If you choose one single token for all your projects, if your token gets leaked, using that token would affect all your projects.

![Screenshot_2022-09-11_14-04-22.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662888981407/6MgaeXUHJ.png align="center")

Once your new API token is generated, make sure you copy that into your clipboard. You'll never be able to access this token again unless you regenerate it.

We're almost done with PyPI. Let's set up the action and finish the automation.

### Create a New Action
Browse your repository. Go to "Settings" tab, and select the "Actions" subcategory from the "Secrets" category in the left bar. Click "New repository secret" and paste the copied PyPI access token. Now, click "Add secret" to store the token in the secrets of your project.

![Screenshot_2022-09-11_14-10-27.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662926455081/Gq2NH9RmK.png align="center")

Navigate to the "Action" tab. Create a new blank action and use the following YAML configuration as your workflow file. We're going to use the make-ready [pypa/gh-action-pypi-publish](https://github.com/pypa/gh-action-pypi-publish) action for this purpose.

```yaml
name: Upload Python Package

on:
  release:
    types: [published]

jobs:
  deploy:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v3
      with:
        python-version: '3.x' # the python version your want to build and upload your package with
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install build
    - name: Build package
      run: python -m build
    - name: Publish new distributions to PyPI
      uses: pypa/gh-action-pypi-publish@release/v1
      with:
        password: ${{ secrets.PYPI_API_TOKEN }}
```

This action starts running once you draft a new release for your repository. There is only one job corresponding to the build and upload process. The `gh-action-pypi-publish` action allows you to upload the newly created package archive to the PyPI servers. All it needs is the API token we saved in the secrets earlier.

### Let's Trigger
For testing terms, navigate to the main page of your repository and go to "Releases".

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663061949545/ZLP0NQp8E.png align="center")

Here you can create a new release for your package which triggers a new workflow run on the lately created action.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663062105552/jLUtazXNR.png align="center")

Choose a proper tag as well as a branch, add some information about your release (or you can simply auto-generate that), and "Publish release". If you navigate to the "Actions" tab now, you'll see that there is a workflow attempting to build and upload your new release to PyPI.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663062404472/ipRkcjxQR.png align="center")

Now whenever you hit "**Draft a new release**" and you publish your release, this event will be triggered automatically and a brand new workflow starts running. The action we used, builds your package and uses `twine`, and tries to upload the newly created build to PyPI using the `PYPI_ACCESS_TOKEN` you're storing as a secret for your actions.

### PyPI Delivery Keynotes
One common issue you might run into during the delivery time (pushing to PyPI) is the duplication of a version. YOU CAN'T have two different releases with the same tag value even if you *remove the release on PyPI*. Your workflow will fail.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663062857363/tTXbr0Poe.png align="center")

### Final Words
This automation could easily speed up your team development so implementing these utilities would save you some time.