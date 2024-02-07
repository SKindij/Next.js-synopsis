# Site Metadata

## title & description
_This attribute is used to set the title of the document._

```typescript
  // @/app/layout.tsx

  // It can be defined as a simple string
  export const metadata = {
    title: 'SKj App',
    description: 'React Framework for the Web',
  }

  // or an optional template object.
  import { Metadata } from 'next'
 
  export const metadata: Metadata = {
    title: {
      template: '%s | App', // can be used to add prefix or suffix to titles defined in child route segments
      default: 'SKj App',  // can be used to provide fallback title to child route segments that don't define title
      absolute: 'Theme Page', // can be used to provide title that ignores title.template set in parent segments
    },
    description: 'React Framework for the Web',
  }
```

## Basic Fields

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

```typescript
  formatDetection: {
    email: false,
    address: false,
    telephone: false,
  },
}  
```

## metadataBase
_It is a convenience option to set a base URL prefix for metadata fields that require a fully qualified URL._






