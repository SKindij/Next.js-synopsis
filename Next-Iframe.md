# Iframe best practices

_When building webpages, developers often need to include resources from other webpages. 
A popular way to retrieve this type of data is with an iframe. 
Using the `<iframe/>` tag, you can easily embed external content from other sources directly into your webpage._

> ! it’s important to embed content only from trusted sources

Keep in mind also that iframes use up additional memory. 
If the content is too large, it can slow down your webpage load time. 
So you should use iframes carefully.

## iframe tag attributes

+ **src**
  - used to set the address of the webpage that you want to embed
  - `<iframe src={"https://i.ytimg.com/vi/${video}/mqdefault.jpg"} />`
  - `<iframe src={"https://www.youtube.com/embed/${video}?"} />`
+ **srcdoc**
  - used to set an inline HTML to embed
  - `<iframe src="https://www.../" srcDoc='<p>Hello from Iframe</p>' />`
  - it will override the src attribute if both are present
+ **width** and **height**
  - use to set the dimensions of our iframe
  - `<iframe width={400} height={300} ></iframe>`
+ **allow**
  - sets the features available to the `<iframe>` based on the origin of the request
  - `<iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture full" />`
+ **title**
  - to set a description for the content in the iframe
  - `<iframe title="YouTube Video" />`
  - it is helpful for accessibility, providing valuable input to screen readers
+ **name**
  - use it to reference the element in JavaScript
+ **sandbox**
  - to set restrictions on the content of the iframe
  - to apply all restrictions, leave the value of the attribute empty
  - `<iframe sandbox='allow-scripts allow-modal' />`
+ **loading**
  - `eager` - the iframe is loaded immediately
  - `lazy` - delays loading until it reaches a calculated distance from the viewport











