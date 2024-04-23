# Querying Remotes

## Search for API products

Searching the in the system API products are called 'services'. These are the Products we can work with. The toolbox can list out the services currently deployed to an environment.

The syntax is `3scale service list <remote>`. Note the output column order, Service ID, service descriptive name and service system name.

~~~
$ toolbox 3scale service list $SOURCE
ID	NAME	SYSTEM_NAME
2	API	api
3	Weather Alerts API	weather-alerts
~~~

We can grep this list if it is long to search for a specific Product.

~~~
$ toolbox 3scale service list $SOURCE | grep -i weather
3	Weather Alerts API	weather-alerts
~~~

From here we can determine the system name for further inspection

## Get system-level API Product Information

You can also use the toolbox to do inspection of higher order objects as well.

The syntax for the command is `3scale service show <remote> <system_name|service_id>`

~~~
$ toolbox 3scale service show $SOURCE weather-alerts
ID	NAME	STATE	SYSTEM_NAME	BACKEND_VERSION	DEPLOYMENT_OPTION	SUPPORT_EMAIL	DESCRIPTION	CREATED_AT	UPDATED_AT
3	Weather Alerts API	incomplete	weather-alerts	1	hosted	admin@3scale.apps.phagerma.lab.upshift.rdu2.redhat.com	Get state-level weather alerts	2023-08-16T19:57:01Z	2023-08-17T15:11:38Z
~~~

Very useful information can be found here, such as the Product administrator's email address, and created / updated times. This information can also be used to make alterations to the API Product right from the command line using the 3scale toolbox, however that is out of the scope of this demo.

## Next Steps

Review the indirect migration approach by [Exporting and Importing](export-import.md) using the toolbox.
