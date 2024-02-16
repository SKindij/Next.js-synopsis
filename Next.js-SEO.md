# Next.js SEO
_In web development, metadata provides additional details about a webpage. Metadata is not visible to the users visiting the page. Instead, it works behind the scenes, embedded within the page's HTML, usually within the <head> element. This hidden information is crucial for search engines and other systems that need to understand your webpage's content better._

## Site Metadata
_Metadata plays a significant role in enhancing a webpage's SEO, making it more accessible and understandable for search engines and social media platforms. Proper metadata helps search engines effectively index webpages, improving their ranking in search results. Additionally, metadata like Open Graph improves the appearance of shared links on social media, making the content more appealing and informative for users._

Next.js has a **Metadata API** that can be used to define your application metadata.

### title & description
_This attribute is used to set the title of the document._

```typescript
  // @/app/layout.tsx

  // It can be defined as a simple string
  export const metadata = {
    title: 'Page Title',
    description: 'A brief description of the page content.',
  }

  // or an optional template object.
  import { Metadata } from 'next'
 
  export const metadata: Metadata = {
    title: {
      // can be used to add prefix or suffix to titles defined in child route segments
      template: '%s | App Title',
      // can be used to provide fallback title to child route segments that don't define title
      default: 'App Title',
      // can be used to provide title that ignores title.template set in parent segments
      absolute: 'Theme Page', 
    },
    description: 'A brief description of the page content.',
  }
```

The `%s` in the template will be replaced with the specific page title.

### Basic Fields

|         layout.tsx & page.js                          |               hnml ``<head>`` output                          |            data assignment                        |
|-------------------------------------------------------|---------------------------------------------------------------|---------------------------------------------------|
|``generator: 'Next.js'``                               |``<meta name="generator" content="Next.js" />``                | information for developers and testers            |
|``applicationName: 'Josh.js'``                         |``<meta name="application-name" content="Next.js" />``         | can be used to identify app in analytics reports  |
|``referrer: 'origin-when-cross-origin'``               |``<meta name="referrer" content="origin-when-cross-origin" />``|   |
|``keywords: ['Next', 'React', 'TS']``                  |``<meta name="keywords" content="Next,React,TS" />``           | used in search engines and directories            |
|``author: [{ name: 'Josh', url: 'https://site.org' }]``|``<meta name="author" content="Josh" />``                      | information about the author                      |
|                                                       |``<link rel="author" href="https://nextjs.org" />``            | ... and a link to his website                     |
|``creator: 'Jiachi Liu'``                              |``<meta name="creator" content="Jiachi Liu" />``               |  information about who created the app            |
|``publisher: 'Sebastian Markbage'``                    |``<meta name="publisher" content="Sebastian Markbage" />``     |  infor about the publisher of the application     |

Any metadata in layout.js will be inherited by all pages that use it.
```typescript
  formatDetection: {
    email: false,
    address: false,
    telephone: false,
  },
}  
```

You can add a custom info for a specific page by adding a `metadata` object to the page itself.
Metadata in nested pages will override the metadata in the parent.

### metadataBase
_It is a convenience option to set a base URL prefix for metadata fields that require a fully qualified URL._

```typescript
  // @/app/layout.tsx
  
  export const metadata = {
    metadataBase: new URL('https://acme.com'),
    alternates: {
      canonical: '/', // <link rel="canonical" href="https://acme.com" />
      languages: {
        'en-US': '/en-US', // <link rel="alternate" hreflang="en-US" href="https://acme.com/en-US" />
        'de-DE': '/de-DE', // <link rel="alternate" hreflang="de-DE" href="https://acme.com/de-DE" />
      },
    },
  }
```

### openGraph
_is a protocol used to determine how your content will be displayed on social networks_

```typescript
  // @/app/layout.tsx
  import { Metadata } from 'next'; // if using TypeScript

  export const metadata: Metadata = {
    openGraph: {
      title: 'Next.js',
      description: 'The React Framework for the Web',
      url: 'https://nextjs.org',
      siteName: 'Next.js',
      images: [
        {
          url: 'https://nextjs.org/og.png',
          width: 1200, height: 630,
          alt: 'Preview image for my site',
        },
      ],
      locale: 'en_US',
      type: 'website',
    },
  };
```

If your application is in production you can easily test it by sending the link to a social like Telegram and check the result./
But if you are in a developing state, I suggest using an extension called
“OGraph Previewer”.

Here's an example of how the file structure for the OG and Twitter images might look:
```go
  ├── app
  │   ├── page.tsx
  │   ├── layout.tsx
  │   ├── favicon.ico
  │   ├── ...
  │   ├── opengraph-image.png
  │   ├── twitter-image.png
  │   ├── opengraph-image.alt.txt
  │   ├── twitter-image.alt.txt
  │   └── ...
  └── ...
```

### robots
_Add or generate a robots.txt file that matches the [Robots Exclusion Standard](https://en.wikipedia.org/wiki/Robots.txt#Standard) in the root of app directory to tell search engine crawlers which URLs they can access on your site._

```typescript
  // @/app/layout.tsx
  import type { Metadata } from 'next'
 
  export const metadata: Metadata = {
    robots: {
      index: false,
      follow: true,
      nocache: true,
      googleBot: {
        index: true,
        follow: false,
        noimageindex: true,
        'max-video-preview': -1,
        'max-image-preview': 'large',
        'max-snippet': -1,
      },
    },
  }
```

