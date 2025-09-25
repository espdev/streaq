Contributing
============

Development
-----------

Contributions to streaQ are always welcome! Most development tasks are in the included ``Makefile``:

- ``make install``: set up the linting environment
- ``make lint``: run ruff to check formatting and pyright to check types
- ``make test``: use the included ``docker-compose.yml`` file to spin up Redis and Sentinel containers, then run test suite. This uses caching so it's faster after the first run. You'll need Docker and compose installed.
- ``make docs``: build the documentation pages with Sphinx
- ``make cleanup``: tear down running Docker containers

If you need to test individual tests instead of the entire suite, you can do this:

.. code-block:: bash

   UV_PYTHON=3.10 docker compose run --rm tests uv run --locked --all-extras --dev pytest -sk 'test_name'

Benchmarks
----------

If you want to run the benchmarks yourself, first install the dependencies:

.. code-block:: bash

   uv add streaq[benchmark]

You can enqueue jobs like so:

.. code-block:: bash

   python benchmarks/bench_streaq.py --time 1

Here, ``time`` is the number of seconds to sleep per task.

You can run a worker with one of these commands, adjusting the number of workers as desired:

.. code-block:: bash

   arq --workers ? --burst bench_arq.WorkerSettings
   saq --quiet bench_saq.settings --workers ?
   streaq --burst --workers ? bench_streaq.worker
   taskiq worker --workers ? --max-async-tasks 32 bench_taskiq:broker --max-prefetch 32

Donating
--------

If you're interested in supporting the ongoing development of this project, donations are welcome! You can do so through GitHub: https://github.com/sponsors/tastyware
