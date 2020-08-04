# SAP Commerce + Spartacus docker-compose script

> Easy-to-run script to run SAP Commmerce with Spatacus storefront *locally*.
> Script focuses on B2B capabilities and Powertools storefront. **Non-production use only.**

## How to run

1. Install docker and docker-compose (https://docs.docker.com/get-docker/, https://docs.docker.com/compose/install/)
1. Download SAP Commerce package (`CXCOM200500P_0-70004955.ZIP`) from SAP Product pages
1. Move `CXCOM200500P_0-70004955.ZIP` into `hybris-b2b-spartacus/hybris-b2b` (if you want to use another version of SAP Commerce, edit `hybris-b2b-spartacus/hybris-b2b/Dockerfile` - replace `CXCOM200500P_0-70004955.ZIP` with your archive filename)
1. Open terminal, navigate to `hybris-b2b-spartacus` folder and run command:
    ```
        docker-compose build
    ```
1. Wait until SAP Commerce initialize (may take up to an hour)
1. Now start the containers:
    ```
        docker-compose up -d
    ```
1. Wait for SAP Commerce to start (may take 10 min)
1. Navigate to http://localhost:4200/ in your browser
    > In some cases you may encounter certificate issue during the first OCC calls. Then just open page https://localhost:9002/occ/v2/powertools-spa/cms/pages?fields=DEFAULT&pageType=ContentPage&pageLabelOrId=homepage&lang=en&curr=USD in your browser and confirm certificate exception)

## Links

* Spartacus Storefront - http://localhost:4200/
* Backoffice - https://localhost:9002/backoffice/ (use `admin`/`nimda` as user/password)
* Smartedit - https://localhost:9002/smartedit/ (use `admin`/`nimda` as user/password)