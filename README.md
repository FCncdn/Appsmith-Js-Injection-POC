# Appsmith-Server-Side-Js-Injection-POC


## Vuln Detail
- Vulnerability type: Server side js injection

- Affected product: Appsmith

- Affected version: v1.7.14 and below

When the application calls the 'currentItem' property of the list widget in the js code, the js injection is caused by not handling the list data properly. An attacker can use this to inject and execute malicious JavaScript code on the server, e.g. to perform dos attacks.

In fact, when the list data contains a semicolon, an error is reported: "UncaughtPromiseRejection: missing ) after argument list", which means that the list component is not handling the data properly and is splicing the list data directly into the js code.

When the list data is user-controllable and 'currentItem' is called in the js code, js injection has occurred.

I have made a simple demo application:
- live demo: https://app.appsmith.com/app/my-first-application/page1-630ebec37e1d9179c33a1950
- demo application: demo_application/My first application.json


You can reproduce the vulnerability in this way.

1. enter poc in any input component on the right
2. click on the button of the first item in the list on the left

![demo-application-overview.png](./img/demo-application-overview.png)

## POC

poc - Denial of Service Attack: `'+ (function(){while(1){}})() +'`

poc - Information Leak: `'+ console.log(appsmith.store) +'`
