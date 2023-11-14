# python-otel-autoinstrumenation
This is an application for Basic Python application to Auto Instrumentation using OpenTelemetry. I have used the https://opentelemetry.io/docs/instrumentation/python/getting-started/ article to make this project. 

We are planning instrument the app.py file using OpenTelemetry

[config.yaml](/app.py) file has multiple secret details which has been masked using xxx. If you still run with the same configuration but it will not export to CCO (https://docs.appdynamics.com/fso/cloud-native-app-obs/en)

Once you make necessary the values with right xxx values then it will start reporting to the CCO tenant too.


Steps to start


1. Start the collector. Download the AppDynamics OpenTelemetry Collector from the download page (https://download.appdynamics.com/) as per your OS.

2. Then start the collector using  config.yaml . It will be something like "./appdotelcol_darwin_amd64 --config config.yaml"
3. Once you start the collector , you need to start the app "opentelemetry-instrument flask run -p 8080"
4. Assumption all the required pip packages are already installed . Refer to https://opentelemetry.io/docs/instrumentation/python/getting-started/
5. Now try accesing the http://127.0.0.1:8080/rolldice on the browser.
6. Refer to the collector logs you will see the traces and span details. As config.yaml has it in debug mode you can something like this

 ```
Span #6
    Trace ID       : aa13323b5229c4075452f131c944e04f
    Parent ID      : 
    ID             : 1553dd903031c11e
    Name           : /rolldice
    Kind           : SPAN_KIND_SERVER
    Start time     : 2023-11-14 22:22:36.866168 +0000 UTC
    End time       : 2023-11-14 22:22:36.866931 +0000 UTC
    Status code    : STATUS_CODE_UNSET
    Status message : 
Attributes:
     -> http.method: STRING(GET)
     -> http.server_name: STRING(127.0.0.1)
     -> http.scheme: STRING(http)
     -> net.host.port: INT(8080)
     -> http.host: STRING(127.0.0.1:8080)
     -> http.target: STRING(/rolldice)
     -> net.peer.ip: STRING(127.0.0.1)
     -> http.user_agent: STRING(Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36)
     -> net.peer.port: INT(63423)
     -> http.flavor: STRING(1.1)
     -> http.route: STRING(/rolldice)
     -> http.status_code: INT(200)
 ```
