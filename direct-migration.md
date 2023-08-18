# Direct Promotion of API Products

When the system you are working from has connectivity to both the source and destination remotes, then the direct migration approach greatly simplifies the process of promotion of Products between systems.

The syntax of the command is `3scale service copy [opts] -s <source-remote> -d <destination-remote> <source-service>`

The system name the product is imported to can be overridden using the option `-t=<value>` if desired.

~~~
$ toolbox 3scale service copy -s  $SOURCE -d $DEST weather-alerts -k
new service id 2555418003667
updated proxy of 2555418003667 to match the original
original service hits metric 8 has 2 methods
target service hits metric 2555419112123 has 0 methods
created 2 missing methods on target service
original service has 1 metrics
target service has 1 metrics
created 0 metrics on the target service
target service missing 1 application plans
Missing 0 plan limits from target application plan 2357356453662. Source plan 10
copy proxy policies
Missing 0 pricing rules from target application plan 2357356453662. Source plan 10
copying all service ActiveDocs
destroying all mapping rules
created 2 mapping rules
~~~

The command copies the complete API product from one system diretly to another without needing to save and transport an export file. It will output the results of the action for review.