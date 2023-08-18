# Exporting and Importing using the toolbox

There may be situation where a direct migration from one environment to another is not possible. Perhaps there is a security restriction that prevents direct connectivity. In this case There is a way to export a product and then transport the exported file to a connected system and import the API product to the target system.

## Exporting API Products

The export command includes Limits defined in the aplication plans, pricing rules, referenced metrics/methods, and linked backends.

The syntax for the command is `3scale product export [options] <remote> <system-name|id>` and the output can either go to stdout, or to a file if the -f option is passed with a filename. When passed with the -f option the command will not return any output.

~~~
$ toolbox 3scale product export -f weather-alerts.yaml $SOURCE weather-alerts
$ ls weather-alerts.yaml 
weather-alerts.yaml
~~~

## Importing API Products

Once you have the export file in a location that has connectivity to the destination instance of 3scale, you can import it into the system.

The syntax for the command is `3scale product import [opts] <remote>`

The option -f will supply the command with the name of the file which contains the exported product. Alternatively it can accept input on stdin.

The import command is idempotent, so it can be run multiple times if there are errors or exceptions. Or if there are changes to your API Product in the source system, creating another export an importing it will update the API Product on the destination system.

When running the import command the output contains the status results of the command.

~~~
$ toolbox 3scale product import -f weather-alerts.yaml $DEST
{
  "weather-alerts": {
    "product_id": 2555418003666,
    "backends": {
      "weather-alerts": {
        "backend_id": 127650,
        "missing_metrics_created": 0,
        "missing_methods_created": 0,
        "missing_mapping_rules_created": 0
      }
    },
    "missing_methods_created": 0,
    "missing_metrics_created": 0,
    "missing_mapping_rules_created": 3,
    "missing_application_plans_created": 0,
    "application_plans": {
      "weather-plan": {
        "application_plan_id": 2357356453660,
        "missing_limits_created": 0,
        "missing_pricing_rules_created": 0
      }
    }
  }
}
~~~

If you have imported a brand new API Product you will not be able to test with it immediately because there will be no subscribed applications. After creating a testing application you can promote the Product to the sandbox, and then publish it to the gateway.

Refer back to the [3scale-toolbox-demo](https://github.com/3scale-demos/3scale-toolbox-demo/) for more information on that.