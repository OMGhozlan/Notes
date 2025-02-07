## Vertical privilege escalation

User gain access to functionality that they are not permitted to access
E.g., a non-administrative user gains access to admin page 

## Parameter-based access control methods

User's access rights or role stored  in a user-controllable location such as :

- A hidden field.
- A cookie.
- A preset query string parameter.

Examples:

`https://insecure-website.com/login/home.jsp?admin=true`
`https://insecure-website.com/login/home.jsp?role=1`

## Horizontal privilege escalation

User can access to resources belonging to another user, instead of their own resources of that type
For example, a user might access their own account page using the following URL:

`https://insecure-website.com/myaccount?id=123`

Modifying the `id` parameter, can lead to access of another user's account page, and the associated data and functions.

#### Note

This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.

In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use globally unique identifiers (GUIDs) to identify users. This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.