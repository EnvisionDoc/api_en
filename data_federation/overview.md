# Data Federation Service Overview

<br />

EnOS Data Federation service enables application developers and data analysts to query data from and write files to multi-source heterogeneous data storage systems. The data federation service APIs support querying the created data reading and writing channels, reading data from storages, and writing files to storages.

<br />

For more information about the Data Federation service, see [Data Federation](/docs/data-asset/en/2.1.0/howto/federation/index.html).


## API List

.. list-table::
   :widths: auto
   :header-rows: 1

   * - API Name
     - Description
   * - `List Channels <list_channels>`__
     - Get the list of channels (Read and Write) to which the application is authorized
   * - `Read Data <read_data>`__
     - Read data by providing SQL query through the specified channel  
   * - `List Jobs <list_jobs>`__
     - Get the data reading jobs or data writing jobs of a specified channel
   * - `Get Job Details <get_job_details>`__
     - Get detailed information of a data reading job or a data writing job
   * - `Write Message <write_message>`__
     - Write message to data source through a specified channel
   * - `Write Chunk File <write_chunk_file>`__
     - Write file chunks to data source through a specified channel


## Common Error Code


<!-- end -->
