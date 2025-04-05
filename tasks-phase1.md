IMPORTANT ❗ ❗ ❗ Please remember to destroy all the resources after each work session. You can recreate infrastructure by creating new PR and merging it to master.
  
![img.png](doc/figures/destroy.png)

1. Authors:

   Group number: 12

   Repository: https://github.com/bujniasz/tbd-workshop-1
   
   Authors:
   - Aleksander Bujnowski
   - Bartłomiej Krajewski
   - Krzysztof Kluczyński
   
2. Follow all steps in README.md.

3. In boostrap/variables.tf add your emails to variable "budget_channels".

![img.png](doc/figures/budget_channels.png)


4. From avaialble Github Actions select and run destroy on main branch.

![img.png](doc/figures/destroy_passed.png)
   
5. Create new git branch and:
    1. Modify tasks-phase1.md file.
    
    2. Create PR from this branch to **YOUR** master and merge it to make new release. 
    
    ![img.png](doc/figures/release.png)


6. Analyze terraform code. Play with terraform plan, terraform graph to investigate different modules.

    The **metascore** module.   

    The metastore module in Terraform is responsible for setting up a Google Cloud Dataproc Metastore service. This service provides a fully managed, scalable metastore for Apache Hive (HMS). It allows metadata management and provides interoperability between the various data processing engines and tools when working with big data on GCP.    

    Key Components:
    - _provider_ - uses the GCP provider (defined in `versions.tf`)
    - _resources_ (described in `main.tf`)
        a) google_dataproc_metastore_service - configures a Dataproc Metastore service with the specified version, network, region, and project name
        b) google_project_service.api-metastore - ensures that the necessary Metastore API is enabled in the project
    - _input variables_ (described in `variables.tf`)
        a) var.metastore_version - specifies the version of the Metastore to be deployed.
        b) var.network - network configuration for the Metastore instance.
        c) var.region - region where the Metastore will be deployed.
        d) var.project_name - the name of the GCP project.
    - _output_ (described in `outputs.tf`)
        a) output.metastore_name - outputs the name of the created Metastore instance

    ![img.png](doc/figures/metastore-graph.png) 

    Graph:
    - Level 1: Root
        - starting point of the entire Terraform graph
        - the "root" node is responsible for initializing the infrastructure creation process
    - Level 2: Provider and Output
        - provider - configures the GCP provider, ensures Terraform has authorization and access to GCP resources
        - output - generates the output name of the created Metastore service, provides the result as an output variable after creation
    - Level 3: Metastore Service Creation
        - responsible for actually creating the Dataproc Metastore instance based on the provided parameters
    - Level 4: Dependent Resources (API and Parameters)
        - guarantees that all required dependencies are activated before creating the primary resource
        - holds configuration data necessary for proper Metastore initialization
    - Level 5: Provider and Project Name
        - provider - direct link to the provider in the context of used variables
        - project name - identifies the project name where the infrastructure will be created

7. Reach YARN UI
   
    ```bash
    gcloud compute ssh tbd-cluster-m --project=tbd-2025l-313595 --zone=europe-west1-d --tunnel-through-iap -- -L 8088:localhost:8088
    ```   

    ![img.png](doc/figures/yarnui.png)    


8. Draw an architecture diagram (e.g. in draw.io) that includes:
    1. VPC topology with service assignment to subnets
    2. Description of the components of service accounts
    3. List of buckets for disposal
    4. Description of network communication (ports, why it is necessary to specify the host for the driver) of Apache Spark running from Vertex AI Workbech
  
    ***place your diagram here***

9. Create a new PR and add costs by entering the expected consumption into Infracost
For all the resources of type: `google_artifact_registry`, `google_storage_bucket`, `google_service_networking_connection`
create a sample usage profiles and add it to the Infracost task in CI/CD pipeline. Usage file [example](https://github.com/infracost/infracost/blob/master/infracost-usage-example.yml) 

   ***place the expected consumption you entered here***

   ***place the screenshot from infracost output here***

10. Create a BigQuery dataset and an external table using SQL
    
    ***place the code and output here***
   
    ***why does ORC not require a table schema?***

11. Find and correct the error in spark-job.py

    ***describe the cause and how to find the error***

12. Add support for preemptible/spot instances in a Dataproc cluster

    ***place the link to the modified file and inserted terraform code***
    
    
