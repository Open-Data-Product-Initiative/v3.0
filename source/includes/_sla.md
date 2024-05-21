# Data SLA

Data Service Level Agreement (SLA) **Object** contains attributes which define the desired and promised quality of the data product. 

A Data Service Level Agreement (SLA) is a contractual agreement between a data service provider and its customers that defines the expected level of service quality, performance, and availability for the data services provided. SLAs outline specific metrics, targets, and responsibilities that both parties agree to adhere to, ensuring accountability and transparency in the delivery of data services.

Defining Data SLAs in a machine-readable format enhances automation, facilitates monitoring, enables real-time compliance tracking, and supports seamless integration with monitoring and alerting systems.

## SLA can be defined with 11 standardized dimensions with Everything as Code monitoring

| <div style="width:150px">SLA Dimension</div>   | Description | 
|---|---|
| **latency** | minimal amount of time before getting any response. |
| **uptime** | Uptime is a measure of system reliability, expressed as the percentage of time a machine, typically a computer, has been working and available. See more https://uptime.is/. |
| **responseTime** | amount of time to process external request. |
| **errorRate** | Maximum tolerated errors in data, percentage. |
| **endOfSupport** | The date at which your product will not have support anymore. |
| **endOfLife** | The date at which your product will not be available anymore. No support, no access. |
| **updateFrequency** | how often data is updates. |
| **timeToDetect** | How fast can you detect a problem? |
| **timeToNotify** | Once you see a problem, how much time do you need to notify your users? |
| **timeToRepair** | How long do you need to fix the issue once it is detected? |
| **emailResponseTime** | How long do you need to respond to email support requests? |

> Template structure of SLA array component:

```yml
 - dimension: selected dimension
    objective: 
    unit: 
    monitoring:
      type:  
      reference: 
      spec:
      
```

Each dimension has objective value, a unit and then *monitoring* "as code" to verify objective. In some cases monitoring is 
not feasable or possible to arrange for various reasons. *Type* attribute indicates which monitoring system is used. *Reference* attribute contains url for reference documentation regarding the monitoring spec. *Spec* contains the actucal "as code" part as YAML or string which can be executed in selected monitoring system as is. **Note!** The "as code" part of the component is the initial step towards embracing Everything as Code paradigm, but is still experimental.

The SLA object is general in nature and should be enough for common (80%) use cases. Note that you can make extensions to the standard with "x-" mechanism in order to fulfill any industry specific needs. The ["Specification extensions"](#specification-extensions) section provides details on how to use this feature. 

Also basic email and phone support information can be expressed inside the SLA component.  

No mandatory attributes at the moment. Optional attributes are listed in own table and an example is given in the right column. 

## Optional attributes and elements

> Example of SLA component usage:

```yml

SLA:
  - dimension: latency
    displaytitle:
      - en: Latency
    objective: 100
    unit: milliseconds
    monitoring:
      type: prometheus
      reference: https://prometheus.io/docs/prometheus/latest/querying/basics/ 
      spec:  # expressed as string or inline yaml
        myTimer.observeDuration();

  - dimension: uptime
    displaytitle:
      - en: Uptime
    objective: 99
    unit: percent
    monitoring:
      type: prometheus
      reference: https://prometheus.io/docs/prometheus/latest/querying/basics/
      spec:  | # expressed as string or inline yaml
        avg_over_time(
          (
            sum without() (up{job="prometheus"})
              or
            (0 * sum_over_time(up{job="prometheus"}[7d]))
          )[7d:5m]
        )    
    
  - dimension: responseTime
    objective: 200
    unit: milliseconds
    monitoring:
      type: prometheus
      reference: https://prometheus.io/docs/prometheus/latest/querying/basics/ 
      spec:  | # expressed as string or inline yaml
        rate(http_server_requests_seconds_sum[$__rate_interval]) / rate(http_server_requests_seconds_count[$__rate_interval])

  - dimension: updateFrequency
    objective: 30
    unit: minutes
    monitoring:
      type: prometheus 
      spec: | # expressed as string or inline yaml
        time() - max_over_time(timestamp(changes(table[5m]) > 0)[1d:1m])

  - dimension: errorRate
    objective: 0.1
    unit: percent
  
  - dimension: endOfSupport
    objective: 01/01/2025 # dd/mm/yyyy
    unit: date

  - dimension: endOfLife
    objective: 01/03/2025 # dd/mm/yyyy
    unit: date

  - dimension: timeToDetect
    objective: 60
    unit: minutes

  - dimension: timeToNotify
    objective: 120
    unit: minutes

  - dimension: timeToRepair
    objective: 24
    unit: hours

  - dimension: emailResponseTime
    objective: 12
    unit: hours

  support:
      phoneNumber: '+971508976456'
      phoneServiceHours: 'Mon-Fri 8am-4pm (GMT)'
      email: support@opendataproducts.org
      emailServiceHours: 'Mon-Fri 8am-4pm (GMT)'
      documentationURL: ''
```



| <div style="width:150px">Element name</div>   | Type  | Options  | Description  |
|---|---|---|---|
| **SLA** | element | - | Binds the SLA related elements and attributes together |
| **dimension** | attribute | string, one of: *latency, uptime, responseTime, errorRate, endOfSupport, endOfLife, updateFrequency, timeToDetect, timeToNotify, timeToRepair, emailResponseTime* | Defines the SLA dimension.   |
| **unit** | attribute  | Options for *unit* are: milliseconds, seconds, minutes, days, weeks, months, years, never, date, null. <br/><br/>  | Name of the quality attribute indicating the timely interval. If date is given, format is dd/mm/yyyy |
| **monitoring** | element | - | Contains the monitoring (computational "as code") structure to validate target state for the selected SLA dimension. |
| **displayTitle** | array | - | Dimension title to be shown is various UIs. Keep it short and sweet. |
| **en** | attribute | [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) defined 2-letter codes | This element binds together other product attributes and expresses the langugage used. In the example this is "en", which indicates that product details are in English. If you would like to use French details, then name the element "fr". The naming of this element follows options (language codes) listed in [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) standard. <br/><br/> You can have product details in multiple languages simply by adding similar sets like the example - just change the binding element name to matching language code. <br/><br/> The pattern to implement multilanguage support for data products was adopted from de facto UI translation practices. The attributes inside this element are commonly rendered in the UI for the consumer and providing a simple way to implement that was the driving reasoning. See for example  [JSON - Multi Language](https://simplelocalize.io/docs/file-formats/multi-language-json/) |
| **type** | attribute | string | monitoring system name name such as Prometheus. The systems enable as code approach to monitor SLA. |
| **spec** | element | YAML or string | contains the as code part for monitoring. Content is intended to be in a form that can be injected as is to defined monitoring system. |
| **reference** | URL | Valid URL | Provide URL for the reference documentation |
| **support** | element | - | Support element describes how the customer can reach for help in case of difficulties in usage, billing, or otherwise. |
| **phoneNumber** | string | valid phone number | The support phone number. Use [E.164](https://www.itu.int/rec/T-REC-E.164/en)  |
| **phoneServiceHours** | string | - | Describes the service hours company provides. Contains information often in week level eg Mon-Fri at 8am - 4pm. |
| **email** | string | valid email address | Email information for support requests. Use [RFC2822](https://datatracker.ietf.org/doc/html/rfc2822) |
| **emailServiceHours** | string | - | Describes the email service hours company provides. Contains information often in week level eg Mon-Fri at 8am - 4pm. |
| **documentationURL** | URL | Valid URL | URL to documentation | 


If you see something missing, described inaccurately or plain wrong, or you want to comment the specification, [raise an issue in Github](https://github.com/Open-Data-Product-Initiative/v3.0/issues)
