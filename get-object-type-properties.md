Goal: list the properties of an object type at runtime

Note that properties are present in our TypeScript types, but type information
is not available at runtime.

"Employee" is, of course, just an example of an object type.

```
import { $Objects } from "@my-app/sdk";
import client from "./client";
import { useEffect, useState } from "react";

function PropertiesList() {
  const [employeeProperties, setEmployeeProperties] = useState<string[]>([]);
  useEffect(() => {
    (async function () {
      const objectType = await client.fetchMetadata($Objects.Employee);
      setEmployeeProperties(Object.keys(objectType.properties));
    })();
  }, []);

  return (
    <ul>
      {employeeProperties.map((prop) => (
        <li key={prop}>{prop}</li>
      ))}
    </ul>
  );
}

export default PropertiesList;
```
