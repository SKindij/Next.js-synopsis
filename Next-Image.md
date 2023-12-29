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








- - -

#### Learn how to use the Next.js Image Component

* YouTube: https://www.youtube.com/watch?v=IU_qq_c_lKA
* Example: https://github.com/vercel/next.js/tree/canary/examples/image-component
* Docs: https://nextjs.org/docs/app/building-your-application/optimizing/images
* API reference: https://nextjs.org/docs/app/api-reference/components/image
