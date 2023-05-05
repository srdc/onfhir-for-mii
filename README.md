# OnFhir.io Setups for Medical Informatics Initiative Germany
This project provide OnFhir.io setups for several FHIR related modules/projects published by Medical Informatics 
Initiative (MII) Germany for different purposes. These setups will provide Docker scripts together with OnFhir configuration 
to easily start up a dedicated FHIR server for the related project. These configurations 
will include the followings;
* a FHIR *CapabilityStatement* specifying the capabilities of the FHIR server, 
* a complete set FHUR StructureDefinition (FHIR Profiles + Extensions) that provides the defined latest FHIR profiles of 
related MII project to enable profile specific validation
* a set of FHIR SearchParameter definitions defining custom search parameters defined for that project
* a set of FHIR ValueSet definitions used in the profiles
* a set of FHIR CodeSystem definitions used in the

Currently, we have only the following setups. You can contact with us if you need a specific related setup.
* *mii-perftest* provides a performance test setup that provides a FHIR server which is optimized for 
population queries on several resource types to demonstrate/test the performance of search and pagination through 
the result set. 

## How to run a setup
You need only Docker installed in your machine for running these setups. For running a specific setup, 
you first need to change the last line of '*docker-compose.yml*'. As shown below, you need to provide the 
path of the folder of the setup to mount it to the onFhir container. In this example, we will run the 
performance test setup where the configurations are given in folder 'mii-perftest'. 
```
   volumes:
      - ./mii-perftest:/usr/local/onfhir/conf
```

Then you can run the following command which will start two containers; one MongoDB container providing the database 
another one onFhir container providing the FHIR server. 
```
docker-compose -p mii up -d
```

You can access the FHIR server from the root URI '*http://localhost:8080/fhir*'. You can test if everything is working 
via the following REST request which will return CapabilityStatement of the server.
```
GET http://localhost:8080/fhir/metadata
```

## Performance Test Setup
In this setup we only support Patient, Condition, Consent, Specimen, Observation, Medication, MedicationAdministration, 
and Procedure. Extra search parameters defined by MII on Consent and Patient are also put into the configuration and are 
supported by the server setup. Database [indexes](./mii-perftest/db-index-conf.json) are configured accordingly for population 
queries planned for these resources (See https://github.com/medizininformatik-initiative/fhir-performance-test/blob/main/performance-tests.json). 



