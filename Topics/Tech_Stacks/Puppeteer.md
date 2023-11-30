
# Puppeteer

Puppeteer is a Node.js library that provides an API to control Chrome or Chromium through the DevTools Protocol. In other words, Puppeteer allows developers and testers to perform automated actions on websites, like clicking links, inputting forms, or clicking buttons. In essence, most things that humans can do in their browsers can be automated by Puppeteer.

## Requirements & Installation

Puppeteer requires Node.js to be installed first. You can download it here: https://nodejs.org/en/.

Then, you can use Puppeteer in your project by running one of the following commands:

```
npm i puppeteer
# or using yarn
yarn add puppeteer
# or using pnpm
pnpm i puppeteer
```
If you are using TypeScript,  the minimum supported version is 4.7.4.

For more information, refer to this link: https://www.npmjs.com/package/puppeteer#getting-started.

## Configuration

Puppeteer has several configurations that have default settings. For a list of all configurations, see this link here: https://pptr.dev/api/puppeteer.configuration.

## Getting started

Below is some example code for starting a Puppeteer browser instance, allowing us to run Puppeteer on the page https://www.utoronto.ca/.

```
const puppeteer = require('puppeteer');

(async () => {
	const browser = await puppeteer.launch();
	const page = await browser.newPage();
	await page.goto(' https://www.utoronto.ca/');
	
	await browser.close();
})();
```

```puppeteer.launch()``` launches a browder instance. You may pass in optional options when needed.

```browser.newPage()``` creates a new Puppeteer page

```page.goto(' https://www.utoronto.ca/')``` is where we specify the url of our page.

```browser.close()``` closes the browser instance process.

For more information, you can follow the tutorial on this site: https://www.freecodecamp.org/news/how-to-use-puppeteer-with-nodejs/.

## Uses of Puppeteer

There are instances in which one might use Puppeteer.

Here are some examples:

1. Query Selectors

Selectors are used to target elements on our web pages to interact with. Queries are the main ways to interact with these selectors using Puppeteer.

To illustrate, we can select an element in several ways:
```  
switch (selectorType) {
      case "xpath":
        console.log(selectorValue);
        await page.waitForXPath(selectorValue);
        const element = await page.$x(selectorValue);

      case "id":
        const formattedId = `#${selectorValue}`
        const element = await page.waitForSelector(formattedId);

      case "name":
        const formattedName = `[name="${selectorValue}"]`
        const element = await page.waitForSelector(formattedName);

      case "className":
        const element = await page.waitForSelector(`.${selectorValue}`);

      case "cssSelector":
        await page.waitForSelector(selectorValue);
        const element = await page.$(selectorValue);
}
```
2. Mouse Actions

We can simulate mouse actions by clicking on elements or using a ```Mouse``` class to control a pointer.

Example:
```  
// clicks on element with the given id
selector = await page.waitForSelector(id);
await selector.click();

 // moves mouse to the coordinates (10, 250)
 await page.mouse.move(10, 250);
```

3. Keyboard Actions

Like the mouse, we can also interact with pages using the keyboard. This is often used for input, such as for forms or for logins.

Example:
```  
// Inputs “hello!” into the element with the given id
selector = await page.waitForSelector(id);
await selector.type(‘hello!’);

// Presses the enter key
 await page.keyboard.press('Enter');
```

4. Emulating devices

We can emulate devices to test web pages or generate screenshots on different devices and page sizes. Below is an example:
```  
// Emulates an iPhone X
await page.setUserAgent('Mozilla/5.0 (iPhone; CPU iPhone OS 11_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/11.0 Mobile/15A372 Safari/604.1');
await page.setViewport({ width: 375, height: 812 });
```

There are several other uses of Puppeteer - visit the following link for more information: https://nitayneeman.com/posts/getting-to-know-puppeteer-using-practical-examples/

## Real-World Examples

Then, what can we do with Puppeteer? Below are a couple examples.

1. Generating automated PDFs and screenshots of websites
2. Assist with automated testing
3. Testing Chrome extensions
4. Web scraping
5. Accessibility testing for websites

Overall, Puppeteer is a great tool to accomplish and utilize browser actions in an automated manner.

## Conclusion

This article provides a brief look at Puppeteer and its features. If you would like to incorporate Puppeteer in your own projects I'd highly recommend using the following resources:

Official Puppeteer Docs: https://pptr.dev/

Puppeteer Examples: https://github.com/puppeteer/puppeteer/tree/main/examples

More Complex Puppeteer Examples: https://github.com/puppeteer/examples

Stack Overflow Questions: https://stackoverflow.com/questions/tagged/puppeteer