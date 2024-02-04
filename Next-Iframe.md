# Iframe best practices

_When building webpages, developers often need to include resources from other webpages. 
A popular way to retrieve this type of data is with an iframe. 
Using the `<iframe/>` tag, you can easily embed external content from other sources directly into your webpage._

> ! it’s important to embed content only from trusted sources

Keep in mind also that iframes use up additional memory. 
If the content is too large, it can slow down your webpage load time. 
So you should use iframes carefully.

### iframe tag attributes

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

## Rendering React components using a portal

_According to the React documentation, portals allow us to render children into a DOM node that exists outside of the parent component’s DOM hierarchy. Basically, [portals let us render children](https://blog.logrocket.com/learn-react-portals-example/) wherever we want to._

``ReactDOM.createPortal(children, domNode, key?)``
  + children = piece of JSX, React Fragment, string, number, an array
  + domNode = DOM location or node to which the portal should be rendered
  + key = optional parameter is a unique string or number

With a React portal, we can choose where to place a DOM node in the DOM hierarchy.

Let’s say we have the following file called MyComponent.js:
```javascript
  function MyComponent() {
    return (
      <div>
        <p style={{ color: "red" }}>Testing to see if my component renders!</p>
      </div>
    );
  }

  export default MyComponent;
```

Now, let’s create a file called CustomIframe.js and write the following code:
```javascript
  import { useState } from 'react'
  import { createPortal } from 'react-dom'

  const CustomIframe = ({ children, ...props }) => {
    const [contentRef, setContentRef] = useState(null)
    const mountNode = contentRef?.contentWindow?.document?.body

    return (
      <iframe {...props} ref={setContentRef}>
        {mountNode && createPortal(children, mountNode)}
      </iframe>
    )
  }

  export default CustomIframe;
```

We created a ref with the useState() Hook, therefore, once the state is updated, the component will re-render. We also got access to the iframe document body, and then created a portal to render the children passed to iframe in its body instead:
```javascript
  import "./SomePage.css";
  import CustomIframe from "./CustomIframe";
  import MyComponent from "./MyComponent";

  export default function SomePage() {
    return (
      <CustomIframe title="A custom made iframe">
        <MyComponent />
      </CustomIframe>
    );
  };
```

You can pass any React app or component as a child of CustomIframe, and it will work just fine! The React app or component will become encapsulated, meaning you can develop and maintain it independently.

## Integrating MUI with React iframes

_By default, MUI uses emotion as its styling engine under the hood, and the generated styles are injected into the parent frame’s head element. However, the styles aren’t inserted into the iframe out of the box because the iframe’s document is different._

You can use the `@emotion/cache` package with the `<CacheProvider/>` component to get emotion to work within embedded contexts like iframes. 

```javascript
  import { useState } from "react";
  import { createPortal } from "react-dom";

  import { CacheProvider } from "@emotion/react";
  import createCache from "@emotion/cache";

  const CustomIframe = ({ children, ...props }) => {
    const [contentRef, setContentRef] = useState(null);
    const cache = createCache({
      key: "css",
      container: contentRef?.contentWindow?.document?.head,
      prepend: true,
    });
    const mountNode = contentRef?.contentWindow?.document?.body;

    return (
      <CacheProvider value={cache}>
        <iframe {...props} ref={setContentRef}>
          {mountNode && createPortal(children, mountNode)}
        </iframe>
      </CacheProvider>
    );
  };

  export default CustomIframe;
```

The generated styles will be inserted into the iframe’s head element. You can also insert them into a DOM node other than the head element.

## Handling events in React iframes

https://blog.logrocket.com/best-practices-react-iframes/











