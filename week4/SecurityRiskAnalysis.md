# Week 4 Security Risk Analysis

## Broken Access Control

### Introduction & Description
Broken Access Control refers to a category of security vulnerabilities where restrictions on what authenticated users are allowed to do are not properly enforced. These flaws allow users to gain unauthorized access to functionality or data, such as accessing other users' accounts, viewing sensitive files, or modifying other users' data. Access control is critical for ensuring that users cannot act outside of their intended permissions. Failures in this area are common and can lead to significant data breaches and unauthorized system modifications.

An example of broken access control could be a web application that uses a predictable pattern for URLs to access user-specific documents, like `https://example.com/documents?user_id=123&doc_id=456`. If the application only checks if the user is logged in but doesn't verify if `user_id=123` actually matches the logged-in user, an attacker could manipulate the `user_id` parameter (e.g., change it to `user_id=124`) to access documents belonging to another user. This is often referred to as Insecure Direct Object Reference (IDOR). Another example is when administrative functions are exposed to non-administrative users simply because the links or buttons to these functions are hidden in the UI, but the backend doesn't actually check the user's role before executing the function.

### Specific Real-World Example
A well-documented real-world example of Broken Access Control involved Facebook (now Meta Platforms) around 2015. Security researcher Laxman Muthiyah discovered a vulnerability in Facebook's Business Ads Manager that allowed him to view and modify photo albums belonging to any Facebook page without authorization. The flaw was an Insecure Direct Object Reference (IDOR) within one of the graph API endpoints used for managing photos. By manipulating the `asset_id` parameter in an API request, he could target albums of other business pages.

Specifically, the API endpoint `POST /<photo_id>/sponsor_image_edit` was intended to allow users to edit sponsored images. However, by substituting the `photo_id` with an ID belonging to another page's album and providing an `asset_id` for a new image, the system would incorrectly grant access, allowing the attacker to add their image to the targeted album. Facebook acknowledged and patched the vulnerability, awarding Muthiyah a bug bounty. This incident demonstrated how broken access control in an API could lead to unauthorized data modification and access, even in a major platform like Facebook.

### Analysis About How to Prevent
Preventing broken access control requires implementing a robust and consistently applied access control mechanism. The primary principle is to deny by default, meaning that access should only be granted if explicitly allowed. Access control decisions should be enforced on the server-side, never relying solely on client-side controls (like hiding UI elements), as these can be easily bypassed. For every request that attempts to access data or perform an action, the server must verify that the authenticated user has the necessary permissions for that specific data or action. This often involves checking user roles and ownership.

Specific prevention techniques include:
- Using attribute-based access control (ABAC) or role-based access control (RBAC) consistently throughout the application
- Instead of using direct object references that can be manipulated (e.g., database keys in URLs), use indirect object references mapped to the user's session or random, unguessable IDs
- Thoroughly test access control mechanisms, including horizontal (accessing other users' data at the same privilege level) and vertical (escalating privileges) privilege escalation attempts
- Rate limiting API requests and logging access control failures can also help detect and respond to attacks attempting to exploit broken access control
- Web application firewalls (WAFs) can provide some defense, but should not be the primary control

### Conclusion
In summary, Broken Access Control is a prevalent and severe security vulnerability that occurs when an application fails to properly enforce restrictions on user actions and data access. This allows attackers to bypass authorization and perform actions as if they were other users or administrators, leading to unauthorized data disclosure, modification, or destruction, as exemplified by the Facebook Business Ads Manager vulnerability. The methodology of such attacks often involves manipulating parameters or exploiting insecure direct object references.

To effectively prevent broken access control, applications must enforce access control checks on the server-side for every request, adopting a "deny by default" stance. Implementing robust mechanisms like RBAC or ABAC, using indirect object references, and conducting rigorous testing are crucial steps. By focusing on centralized and consistently applied access control logic, developers can significantly mitigate the risks associated with these vulnerabilities.

### Verification Sources
- [Hacking Facebook Photo Album](https://thehackernews.com/2015/02/hacking-facebook-photo-album.html)
- [Facebook Photo Album Vulnerability Bug Bounty](https://www.theverge.com/2015/2/12/8026159/facebook-photo-album-vulnerability-bug-bounty)
- [Facebook Bug Let Researcher Delete Any Public Photo](https://www.businessinsider.com/facebook-bug-delete-any-photo-12500-bounty-laxman-muthiyah-2015-2?op=1)
- [Bug Let Researcher Delete Any Public Facebook Photo](https://www.pcmag.com/news/bug-let-researcher-delete-any-public-facebook-photo)

### Prompt
---
*Generated using Gemini 2.5 Pro with the prompt: "Using the requirements from this document can you show me what a good assignment would look like with all important topics covered for this topic: Broken Access Control"*