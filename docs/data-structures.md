<!--
 Copyright 2019 PayPal Inc

  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

To allow model execution to be scalable and robust, the framework internally uses streaming oriented data structures

# Data containers

Data structures are used for holding historical window data. The containers API exposes efficient statistics (e.g. average, stdev) and internally cache calculations to avoid re-computation and boost performance

**Container types**

Uniform Sampling (default) – stores only a uniform sample of the data points in a window, uses Reservoir Sampling algorithm

Sorted Uniform Sampling – same as Uniform Sampling but points are also ordered, supports more advanced statistics like median and percentiles approximation
*currently supports only  long values

Raw – stores all data points, memory intensive and not recommended for production

**Models that use data containers have additional parameters:**

|param|default|description|
|-----|-------|-----------|
|containerType|Uniform Sampling| the type of container to use|
|maxWindowCapacity|10,000| the maximal raw events to keep in each window container|

# Data Frame API

We extend Spark's DataFrame API by adding the workload to the computation graph.

```
// import the Dataframe api extension
import com.paypal.risk.platform.veda.analytics.Implicits._
 
// add workload to computation
df.detectAnomalies(workload)

```
