## Ampified Magazine

## Basic requirements for AMP-ified pages
- no external files other than media (e.g. images, videos) are loaded
- therefore only inline styles are allowed
- external js sources (e.g. tracking, zendesk support, social sharing) need to be implemented using amp-components
- pages need to have a canonical link to the already existing pages to gain their ranking and authority
- to get shown in the ranking, pages need to be validated against a validator

## Main goal
Find out, what needs to be done, to improve the load time of static pages in babbel. Our example is the best visited
[magazine page](https://www.babbel.com/en/magazine/the-10-most-spoken-languages-in-the-world).
3 main questions need to be answered:

1. Can we use this approach at all without reducing the required functionality (tracking, external services (zendesk, disqus), social sharing)?
2. What issues do we have with the current build process and how could they be mitigated?
3. What are the next steps to be taken to get there?


## 1. Can we use this approach at all without reducing the required functionality
Yes, **BUT** there is a lot that still needs to be tackled.

## 2. What issues do we have with the current build process and how could they be mitigated?
TL;DR
Tracking could not be implemented due to missing prerequisites.
In the build process, several changes need to be implemented (statamic's markdown parser), duplication of content can not be avoided and steps in between need to be added to get to the wished result...

During the implementation and evaluation we ran into many issues, that will be listed here:

- the styles served for the magazine are so huge, that we do not get a valid page for it => use cascada.css
- images inside content
  - can not be rendered as `amp-img` tags yet (needs to be implemented into the parser used by statamic)
  - dimensions are unknown, which also makes the page not validated
- for every external service specific prerequisites need to be met
  1. google tag manager
    - there is an existing component [already available](https://www.ampproject.org/docs/reference/components/ads/amp-analytics)
    - special `AMP` container needs to be setup on GTM
  2. disqus
    - there is an existing component [already available](https://github.com/disqus/disqus-install-examples/tree/master/google-amp)
    - special account (valid for multiple domains needs to be available) needed
    - serving an custom, external JS from another domain
  3. social sharing
    - there is an existing component [already available](https://www.google.de/amp/s/www.ampproject.org/docs/reference/components/social/amp-social-share)
    - can be integrated easily
  4. internal custom tracking
    - no component available
    - needs to be developed in contact with google
