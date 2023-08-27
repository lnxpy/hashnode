---
title: "A Guide to Creating MindsDB Integrations"
datePublished: Sun Aug 27 2023 18:46:22 GMT+0000 (Coordinated Universal Time)
cuid: clltsxfbn000009jp3xdgau3t
slug: a-guide-to-creating-mindsdb-integrations
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693135720884/0c08a555-3ea4-422d-8253-f1b22144f0d9.png
tags: opensource, databases, integration, mindsdb, contribution-to-open-source

---

In this article, we're going to talk about how you can make new handler integrations into the [MindsDB](https://github.com/mindsdb/mindsdb) codebase.

### TL;DR

[MindsDB](https://mindsdb.com) is a cloud database service with a lot of AI and data integrations that help you design, train, and predict over the cloud!

MindsDB's community has always been welcoming all contributions over their repositories. Since they have such nice support for their products alongside their active community, I decided to write down this quick tutorial on how you can contribute to MindsDB by creating your handler integrations.

This guide is created for those who want to contribute to `mindsdb/mindsdb` so without further ado, let's talk about the steps.

### Fork & Clone

First thing first, make sure that you have `mindsdb/mindsdb` forked and cloned on your machine. Change your directory to where the codebase is on.

### Create A Handler

I've written a tool that helps you create MindsDB handlers with a few question answerings. It's basically a Cookiecutter template that provides whatever you may need during your handler development. Follow the steps to create a basic handler template for yourself.

#### 1\. Install Cookiecutter

Make sure you have `Python` and `pip` installed and updated on your machine and install the `cookiecutter` package via the following command.

```bash
pip install -U cookiecutter
```

To test it out and find out whether the installation was successful, run it with the `-V` flag.

```bash
cookiecutter -V
```

#### 2\. Generate the template

Now, it's time to use my tool called [`lnxpy/cookiecutter-mindsdb`](https://github.com/lnxpy/cookiecutter-mindsdb) to generate a simple handler for yourself. MindsDB stores all the handlers in `mindsdb/integrations/handlers/` so we need to put our handler in that path too. Keep in mind that we've already changed our directory to `mindsdb/`.

```bash
cookiecutter gh:lnxpy/cookiecutter-mindsdb -o mindsdb/integrations/handlers/
```

After running the above command, it tries to retrieve the content of the cookiecutter template and then, it asks you a bunch of questions in order to create the most suitable handler for you. The following table helps you answer the questions accurately.

| Question | Description | Type | Examples |
| --- | --- | --- | --- |
| Handler name | Name of your handler | `str` | `PyPI` - `Google` - `GitHub Copilot` |
| Handler slug | Slug version of your handler name | `str(slug)` | `[Leave this empty]` |
| Description | A short description of your handler | `str` | `MindsDB handler for doing some awesome things` |
| Author name | Your name | `str` | `John Doe` - `Sadra` - `Sara` |
| Version | Starting version of your handler | `str` | `0.0.0` - `1.0.0` - `1.0.0-b1` - `2023.03` |
| Has dependencies | Whether your handler has dependencies (`requirements.txt`) | `y/n` | `y` - `n` |
| Need version bumper | Whether you want to use `bump2version` for version management of your handler | `y/n` | `y` - `n` |

When you see the following message, it means that your handler has been created successfully in that specific handler's path of MindsDB.

```bash
+ Sample Handler is created successfully!
```

If you navigate to the path to your handler, a quick tree view of your handler would be like the following scheme.

```bash
<name>_handler/
├── README.md
├── __about__.py
├── __init__.py
├── <name>_handler.py
├── <name>_tables.py
└── icon.svg

1 directory, 6 files
```

The files that need to be updated are `README.md`, `<name>_handler.py`, `<name>_tables.py`, and `icon.svg`. If your handler has any dependencies, once you've installed the dependencies, don't forget to update the `requirements.txt` file and put the output of `pip freeze` command into it as follows.

```bash
pip freeze > requirements.txt
```

In the next two sections, we'll be talking about each file and method so that you can write your handlers in a flash!

### Develop Your Handler

In this section, we'll be going through both `_handler.py` and `_tables.py` files and their instructions. To run a local instance of MindsDB, create a virtual environment, install the dependencies, and run it with the following commands.

```bash
$ virtualenv venv && source venv/bin/activate
$ pip install -e .
$ pip install -e ".[dev]"
```

The following command runs the MindsDB engine on your local machine and shows the exact port that it's accessible from.

```bash
$ python -m mindsdb
```

Let's dive into the `<name>_handler.py` and `<name>_tables.py` files that contain most of our implementations. In my case, my handler name is `Sample` so I'll bring examples and practices based on this name.

### Handler Development

The following handler stub structure is generated in `sample_handler.py` by default.

```python
class SampleHandler(APIHandler):
    def __init__(self, name: str, **kwargs) -> None: ...
    def check_connection(self) -> StatusResponse: ...
    def connect(self): ...
    def native_query(self, query: str) -> StatusResponse: ...
```

We'll go through each method and the way you should implement them.

### `SampleHandler.__init__()` Method

The `SampleHandler.__init__()` method gets triggered on the following `CREATE DATABASE` query execution over in the dashboard.

```sql
CREATE DATABASE sample_db
WITH ENGINE = 'sample';
```

Inside this method, you should create the tables that you need. As you can see, there is already a `SampleTable` class created there by default. Create your required tables inside `<name>_tables.py`, import them into the `<name>_handler.py` and add them in `_tables` variables inside the `__init__()` method.

```python
...
from mindsdb.integrations.handlers.sample_handler.sample_tables import SampleTable


class SampleHandler(APIHandler):
    def __init__(self, name: str, **kwargs) -> None:
        """initializer method

        Args:
            name (str): handler name
        """
        super().__init__(name)

        self.connection = None
        self.is_connected = False

        _tables = [
            SampleTable,
            #...
        ]

        for Table in _tables:
            self._register_table(Table.name, Table(self))
```

Notice that there are two attributes called `self.connection` and `self.is_connected` inside the initializer method. We need to set them from within the `connect()` and `check_connection()` methods.

### `SampleHandler.check_connection()` Method

This method has to return a `StatusResponse(True/False)` object meaning the handler is still available to access the third-party for the further communications. This method is also where we set a bool value for `self.is_connected`. A quick sample for this method would be like this.

```python
    ...
    def check_connection(self) -> StatusResponse:
            response = StatusResponse(False)
            
            try:
                _ = requests.get("https://google.com", timeout=5).raise_for_status()
                response.success = True
                self.is_connected = True
            except requests.exceptions.RequestException as e:
                response.error_message = e
    
            return response
```

### `SampleHandler.connect()` Method

This method is where you have to put a value into the `self.connection` attribute. A good example for this would be returning a `requests.get()` object.

```python
    ...
    def connect(self) -> Callable[..., Response]:
        """making the connectino object

        Returns:
            Callable: requests.get
        """
        self.connection = requests.get
        return self.connection
```

We need the value that this method puts into the `self.connection` later in our `sample_tables.py`.

### Tables Development

Now, let's see the `sample_tables.py` and the methods and classes that live there. You can copy and paste your tables from the initial `SampleTable` or even modify it. The first step is to specify each table's columns and names. You can do this by changing the `name` and `columns` attributes of each class.

```python
class SampleTable(APITable):
    name: str = "sample"
    columns: List[str] = ...

    def __init__(self, handler: APIHandler): ...
    def select(self, query: ast.Select) -> pd.DataFrame: ...
    def get_columns(self, ignore: List[str] = []) -> List[str]: ...
```

There is a `SampleTable.select()` method defined by default. This is the only method that you probably need to change. This method is called whenever someone queries a `SELECT` statement over your table. All the parameters and clauses that the user specifies can be reachable from the `query` attribute.

You can define other methods such as `SampleTable.insert()` for the `INSERT INTO` purpose.

### Don't Forget to..

I highly recommend you take a look over other the handler integrations' source code. They'll give you a nice point of view about the components and how they're supposed to be implemented. As references, I suggest the [MediaWiki Handler](https://github.com/mindsdb/mindsdb/tree/staging/mindsdb/integrations/handlers/mediawiki_handler) and [PyPI Handler](https://github.com/mindsdb/mindsdb/tree/staging/mindsdb/integrations/handlers/pypi_handler) which I maintain!

What's more, @[Artem Veremey](@aiav) has published ["Building a New MindsDB Integration: A Step-by-Step Guide With Examples From the GitHub Handler"](https://aia.hashnode.dev/building-a-new-mindsdb-integration-a-step-by-step-guide-with-examples-from-the-github-handler) article over on his blog that might give you more perspectives and ideas about this integration. Shout out to him!

### Conclusion

In this quick tutorial, we talked about MindsDB and the way you can ship your desired handlers over it via a simple Cookiecutter template. Hopefully, this tutorial has helped you build your integrations easier.