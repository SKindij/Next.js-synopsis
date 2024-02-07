# Metadata Fields

## title
_This attribute is used to set the title of the document._

```typescript
  // @/app/layout.tsx

  // It can be defined as a simple string
  export const metadata = {
    title: 'SKj App',
  }

  // or an optional template object.
  import { Metadata } from 'next'
 
  export const metadata: Metadata = {
    title: {
      template: '%s | App', // can be used to add prefix or suffix to titles defined in child route segments
      default: 'SKj App',  // can be used to provide fallback title to child route segments that don't define title
      absolute: 'Theme Page', // can be used to provide title that ignores title.template set in parent segments
    },
  }
```

## description









