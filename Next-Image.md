# Next-Image

> Images account for a huge portion of the typical website’s page weight and can have a sizable impact on your website's LCP performance.

Next.js `<Image />` extends HTML `<img>` element with features for automatic image optimization:
+ Size Optimization:
  - Automatically serve correctly sized images for each device, using modern image formats like WebP and AVIF.
+ Visual Stability:
  - Prevent layout shift automatically when images are loading.
+ Faster Page Loads:
  - Images are only loaded when they enter the viewport using native browser lazy loading, with optional blur-up placeholders.
+ Asset Flexibility:
  - On-demand image resizing, even for images stored on remote servers

```tsx
  import Image from 'next/image'
 
  export default function Page() {
    return (
      <Image src="/profile.png"
        width={500} height={500}
        alt="Picture of the author"
      />
    )
  }
```

### Local Images

To use it, `import` your `.jpg`, `.png`, or `.webp` image files.

```tsx
  import Image from 'next/image'
  import profilePic from './me.png'
 
  export default function Page() {
    return (
      <Image src={profilePic}
        alt="Picture of the author"
        // width={500} automatically provided
        // height={500} automatically provided
        // blurDataURL="data:..." automatically provided
        // placeholder="blur" // optional blur-up while loading
      />
    )
  }
```

> **Warning:** Dynamic `await import()` or `require()` are not supported.
> The import must be static so it can be analyzed at build time.

### Remote Images

To it, the `src` property should be a URL string.

Since Next.js does not have access to remote files during the build process, you'll need to provide the width, height and optional blurDataURL props manually.

```tsx
  import Image from 'next/image'
 
  export default function Page() {
    return (
      <Image
        src="https://s3.amazonaws.com/my-bucket/profile.png"
        alt="Picture of the author"
        width={500}
        height={500}
      />
    )
  }
```

> To safely allow optimizing images, define list of supported URL patterns in `next.config.js`. 

#### remotePatterns

```ts
  // next.config.js
  module.exports = {
    images: {
      remotePatterns: [
        {
          protocol: 'https',
          hostname: 'example.com',
          port: '',
          pathname: '/account123/**',
        },
        {
          protocol: "https",
          hostname: "your-website.com",
        },
        {
          protocol: "http",
          hostname: "localhost",
        },
      ],
    },
  }
  /* src property of next/image must start with:
       https://example.com/account123/
       https://your-website.com
       http://localhost
```

#### domains
> Deprecated since Next.js 14 in favor of strict `remotePatterns` in order to protect your application from malicious users. 

Only use `domains` if you own all the content served from the domain.

```ts
  // next.config.js
    module.exports = {
      images: {
        domains: ['assets.acme.com'],
      },
    }
```

#### loaderFile

```ts
  // next.config.js
  module.exports = {
    images: {
      loader: 'custom',
      loaderFile: './my/image/loader.js',
    },
  }
```





- - -

#### Learn how to use the Next.js Image Component

* YouTube: https://www.youtube.com/watch?v=IU_qq_c_lKA
* Example: https://github.com/vercel/next.js/tree/canary/examples/image-component
* Docs: https://nextjs.org/docs/app/building-your-application/optimizing/images
* API reference: https://nextjs.org/docs/app/api-reference/components/image
