---
layout: post
title:  "Rest API Design Rules"
date:   2012-03-29 1:10:00
categories: REST
---

I'have found some important rules need to consider for REST API design.

1. Forward slash separator (/) must be used to indicate a hierarchical relationship.
2. A trailing foreword slash (/) should not be included in URLs.
3. Hyphens (-) should be used to improve the readability of URLs.
4. Underscore should not be used in URLs.
5. Lower case letters should be preferred in url paths
6. File extensions should not be  included in URLs
7. Consistent sub domain names should be used for your api. I.e. http://API.domain.com
8. Consistent subdomain names should be used for your client developer portal. I.e.  http://developer.domin.com
9. A singular noun should be used for document names.(a resource, an object instance or database records.)
10. A plural noun should be used for collection names (collection of resource)
11. A verb or verb phrase should be used for controller name (functions or actions)
12. Variable path segments may be substituted with identity based value. I.e http://API.domin.com/users/(user Id) 
13.CURD functions name should not be used in URLs.
14.the query parameter of URL may be used to filter collections.
15. The query parameter of a URLs should be used to paginate collections results.