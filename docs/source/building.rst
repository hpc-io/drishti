Build Instructions
===================================

Drishti framework comprises of multiple modules that can be used by themselves or in tandem.

The visualization of Darshan logs a Darshan log file collected with tracing data. The Darshan eXtended Tracing (DXT) support is disabled by default in Darshan. To enable tracing globally for all files, you need to set the ``DXT_ENABLE_IO_TRACE`` environment variable as follows:

.. code-block:: bash

    export DXT_ENABLE_IO_TRACE=1

To enable tracing for particular files you can refer to the Darshan's documentation page.

Drishti can also provide insights and recommendations for Darshan profiling logs (those without DXT support enabled) or Recorder traces.

-----------------------------------
Installing through git
-----------------------------------

.. note::

    In Perlmutter (NERSC) you might need to load Darshan and Python modules if they are not already loaded. For other systems, please refer to their documentation to use the correct module name.
    
    .. code-block:: bash

        module load python
    
    .. code-block:: bash
        
        module load darshan
        
.. note::

    In Summit at OLCF you need to follow this set of instructions.
    
    .. code-block:: bash
    
        module load python
    
        conda create -n py310-dxt python=3.10
        source activate py310-dxt
        conda install arrow-cpp=10.0.1 pyarrow=10.0.1

        git clone https://github.com/hpc-io/dxt-explorer
        cd dxt-explorer

        pip install .

        dxt-explorer samples/YOUR-DARSHAN-FILE.darshan

        conda deactivate

Run the below command to install some required Python libraries:

.. code-block:: bash

    pip install -r requirements.txt

Then install dxt-explorer using the following command:

.. code-block:: bash

    pip install .

-----------------------------------
Docker Image
-----------------------------------

You can also use a Docker image already pre-configured with all dependencies to run Drishti:

.. code-block:: bash

    docker pull hpcio/drishti-framework

Since we need to provide input files and access the generated ``.html`` files, make sure you are mounting your current directory in the container and removing the container after using it. You can pass the same arguments described above, after the container name (``dxt-explorer``).

.. code-block:: bash

    docker run --rm --mount \
        type=bind,source="$(pwd)",target="/dxt-explorer" \
        dxt-explorer darshan/<FILE>.darshan

