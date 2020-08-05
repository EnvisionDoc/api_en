# Prediction Model Service Overview

<br />

The predictive model service is a service that is automatically created by deploying  "predictive" machine learning algorithm models via the EnOS Algorithm Model Hosting service. The service can be invoked by providing the service ID and business parameters of the deployed model.    

## API List

.. list-table::
   :widths: 40 60
   :header-rows: 1

   * - Operation Name
     - Description
   * - `Machine Learning Forecast <machine_learning_forecast>`__
     - Get the predition results of the deployed machine learning algorithm model.


## Error Code

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - Code
     - Error Information
     - Description
   * - 61951
     - parameter is not correct
     - The provided parameters are not valid.
   * - 61952
     - serviceId not found
     - The provided service ID is not found.
   * - 61953
     - Prediction service is not running
     - Prediction service exception (service is not running)
   * - 61954
     - Internal service error
     - Internal service exception

<!-- end -->
