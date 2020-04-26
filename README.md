# DBT-Docker

This repo contains a `Dockerfile` to build
[Docker](https://www.docker.com) image for building templated SQL transforms
using the Python [dbt](https://docs.getdbt.com/docs/introduction) package. The
foundation of the image is the [Miniconda](https://conda.io/miniconda.html)
environment management system developed by
[Anaconda, Inc](https://www.anaconda.com/). Core packages included in the
image include:
* CPython (3.7)
* Numpy
* Pandas
* [dbt](https://getdbt.com)
* [dbt-sqlserver](https://github.com/mikaelene/dbt-sqlserver), which extends dbt for use with Microsoft SQL Server 2016 and up.
* [dbt-utils](https://hub.getdbt.com/fishtown-analytics/dbt-utils/0.1.7/) ([repo](https://github.com/fishtown-analytics/dbt-utils/tree/0.1.7/)), which adds a few dozen utility macros to those provided by dbt itself.
* [dbt-event-logging](https://github.com/fishtown-analytics/dbt-event-logging), which adds pre-/post-hooks for logging dbt runs and events.

Additional packages are included for:
* Documentation (Sphinx)
* Testing (pytest, coverage)
* Linting (pylint)
* Environment management (python-dotenv)
* Database connectivity (sqlalchemy, pyodbc)

## Usage

To instantiate an ephemeral container from the image, mount the current
directory within the container, and open a bash prompt within the `base` conda
Python environment:

```bash
docker run -it --rm -v $(pwd):/home/docker/work blueogive/dbt-docker:latest
```

You will be running as root within the container, but the image includes the
[gosu](https://github.com/tianon/gosu) utility. This allows you to conveniently execute commands as other users:

```bash
gosu 1000:100 python myscript.py
```

## Best Practices

The dbt development team has created a thoughtful list of
[best practices](https://docs.getdbt.com/docs/guides/best-practices) for using
dbt based on their experience developing and using the product.

Contributions are welcome.
