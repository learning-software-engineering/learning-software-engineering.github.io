# URL Sanitization: What is it? Why should we do it? How do we do it?

## Table of Contents:
### [Introduction](#introduction-1)
### [What is sanitization and why does it matter?](#what-is-sanitization-and-why-does-it-matter-1)
### [How should we sanitize URLs?](#how-should-sanitize-urls-1)
### [Examples of how to use](#examples-of-how-to-use-1)
### [How to test the implementation of your sanitization function](#how-to-test-the-implementation-of-your-sanitization-function-1)
### [Errors you might encounter](#Errors-you-might-encounter-1)


## Introduction

In today's digital landscape, web applications are essential tools for businesses and individuals. However, they are also susceptible to various cyber threats, including attacks through manipulated URLs. To safeguard against potential vulnerabilities, it's imperative to understand and implement proper URL sanitation practices. As a student learning software engineering, sanitization of URLs is a key concept when building a new web application.


## What is sanitization and why does it matter?

URL sanitation is the process of validating, cleaning, and securing incoming URLs in a web application. There should be some level of sanitation for every web application. Here are some reasons why it is needed:

-Guarding against Security Threats: Unsanitized URLs can be gateways for security threats such as cross-site scripting (XSS) (This is the process of injecting malicious scripts in websites. More information can be found here: https://owasp.org/www-community/attacks/xss/), SQL injection (Malicious code used to access and modify backend databases. More information about this can be found here: https://www.imperva.com/learn/application-security/sql-injection-sqli/#:~:text=SQL%20injection%2C%20also%20known%20as,lists%20or%20private%20customer%20details.), and other malicious attacks. Sanitizing URLs mitigates these risks.

-Protecting User Data: Proper sanitation ensures the safety of user data by avoiding potential exposure to attackers who might exploit vulnerabilities in URLs to access sensitive information. This is vital for owning a website that users can trust.

-Maintaining Application Integrity: By sanitizing URLs, you maintain the integrity and functionality of your application, reducing the risk of unexpected behaviors or compromises.


## How should we sanitize URLs?

Implementing URL sanitation involves several key steps and best practices:

Input Validation: Validate incoming URLs against a strict set of rules and expected patterns. Ensure they conform to standard URL formats and accepted protocols (HTTP/HTTPS).

Encoding and Escaping: Encode special characters in URLs using proper encoding mechanisms such as [encodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent) in JavaScript or server-side functions like urlencode() in PHP. Additionally, escape output when displaying URLs on web pages to prevent interpretation as executable code. Just remember that you may have to decode the URL parameters after if you need parameter values in your code. This can be done using [decodeURIComponent()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent).

Whitelisting: Define a whitelist of allowed characters, protocols, and URL patterns. Reject any URL that does not match the predefined criteria, effectively filtering out potentially harmful input. Here is an example of what characters could be on the whitelist: (A-Za-z0-9-._~:/?#[]@!$&'()*+,;=%). Notice that this does not include angle brackets (<>) or curly braces ({}) as those are not needed in a URL and can be used maliciously.

Regular Expressions: Use regular expressions to match and filter URLs based on expected patterns. Regular expressions can help validate and sanitize URLs effectively.

Utilize Security Libraries: Leverage trusted URL sanitization libraries or frameworks available in your programming language or framework. These libraries often provide specific methods to clean and validate URLs effectively. The best one I know of is the [sanitize-url](https://www.npmjs.com/package/@braintree/sanitize-url) library. This is good for general sanitization, but if you need specific cases checked, then it may be more effective to build a sanitization function from scratch.


## Examples of how to use

Example of using sanitize-url library:

First, you have to install the library using this: npm install -S @braintree/sanitize-url

Below are a couple of examples of implementations for sanitization methods. Remember if you are using this to sanitize URL parameters, the parameters should be sanitized before used for anything else.

```javascript
var sanitizeUrl = require("@braintree/sanitize-url").sanitizeUrl;

sanitizeUrl("https://example.com"); // 'https://example.com'
sanitizeUrl("http://example.com"); // 'http://example.com'
sanitizeUrl("www.example.com"); // 'www.example.com'
sanitizeUrl("mailto:hello@example.com"); // 'mailto:hello@example.com'
sanitizeUrl(
  "&#104;&#116;&#116;&#112;&#115;&#0000058//&#101;&#120;&#97;&#109;&#112;&#108;&#101;&#46;&#99;&#111;&#109;"
); // https://example.com

sanitizeUrl("javascript:alert(document.domain)"); // 'about:blank'
sanitizeUrl("jAvasCrIPT:alert(document.domain)"); // 'about:blank'
sanitizeUrl(decodeURIComponent("JaVaScRiP%0at:alert(document.domain)")); // 'about:blank'
// HTML encoded javascript:alert('XSS')
sanitizeUrl(
  "&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041"
); // 'about:blank'
```

The more recommended method is to make your own function, here is an example of one that I made:

```javascript
export const sanitizeInput = (input, isUrl = false) => {
  if (typeof input !== 'string') {
    return input
  }
  let paramInput = input
  let splitUrl
  if (isUrl && input) { //splitting url so we only sanitize parameters
    splitUrl = input.split('?')
    paramInput = splitUrl.length > 1 ? splitUrl[1] : ''
  }
  //force incoming url to math this regex pattern
  const sanitizedInput = paramInput.replace(/[^a-zA-Z0-9\s.,!?_&=%<>"']/g, '')
  // Input encoding
  const htmlEntities = {
    '<': '&lt;',
    '>': '&gt;',
    '"': '&quot;',
    "'": '&#39;',
  }

  const encodedInput = sanitizedInput.replace(/[<>"']/g, char => htmlEntities[char])

  // HTML tag filtering
  const filteredInput = encodedInput.replace(/<\/?script>/gi, '')
  if (isUrl && input) { // recombining url
    const sanitizedPart = splitUrl.length > 1 ? (`?${filteredInput}`) : ''
    return splitUrl[0] + sanitizedPart
  }
  return filteredInput
}
```
Of course, every situation is different, and you might need to add or remove different characters from your whitelist, or you may have to add more encoding and decoding. This document specifically talks about URL sanitization, but this method is also effective for any type of data coming into your application. This even includes text fields that users enter data into.


## How to test the implementation of your sanitization function


To test your new function, you will want to pass different URLs into the function (this example is for JavaScript React). Here are a couple of examples for sanitizeInput():
```javascript
describe('sanitizeInput function', () => {
  it('should return the input string as is when it is not a string', () => {
    const input = 123; // Input is a number
    const result = sanitizeInput(input);
    expect(result).toEqual(input);
  });

  it('should sanitize URL parameters and remove unwanted characters', () => {
    const inputUrl = 'https://example.com/?param1=<script>alert("XSS")</script>&param2=abc';
    const sanitizedUrl = sanitizeInput(inputUrl, true);
    expect(sanitizedUrl).toEqual('https://example.com/?param1=&param2=abc');
  });
});
```

## Errors you might encounter

When the sanitization change is merged, check if the function is working correctly. This can be done by adding an alert in a URL for your website (example: 'https://example.com/?param1=<script>alert("XSS")</script>&param2=abc'). If an alert pops up on the window, then this means the sanitization is not working correctly and you are probably missing something important in your sanitization function (you might have to alter your whitelist to include less characters).

If you notice that some of the URL parameters are becoming altered by this sanitization, then there could be 2 reasons for this:

-Your whitelist in the sanitization function is too strict and is not letting normal characters pass through.

-You are using improper characters in your URL parameters. Here is a [good reference](https://www.freecodecamp.org/news/url-encoded-characters-reference/) which describes which characters should and should not be put in URL parameters.