Goal: greet the current user by name in your app

1. Ensure you've enabled admin read permissions in developer console

2. Update your OAuth2 login flow to request the admin read permission

client.ts or createClientAndAuth.ts (wherever you create your auth):

```
const scopes = [
	"api:ontologies-read",
	"api:ontologies-write",
	"api:admin-read",
	"api:mediasets-read",
	"api:mediasets-write"
];
export const auth = createPublicOauthClient(
  clientId,
  url,
  redirectUrl,
  true,
  undefined,
  window.location.toString(),
  scopes,
);
```

3. Install the foundry.admin package

terminal:

```
npm install @osdk/foundry.admin
```

4. Define your greeting component

Greeting.tsx:

```
import client from "./client";
import { Users } from "@osdk/foundry.admin"
import { useEffect, useState } from "react";

function Greeting() {
  const defaultName = "human";
  const [currentUser, setCurrentUser] = useState(defaultName);
  useEffect(() => {
    (async function () {
      const user = await Users.getCurrent(client);
      setCurrentUser(user.givenName || defaultName);
    })();
  }, []);

  return <div>Hello {currentUser}!</div>;
}

export default Greeting;
```
