## SWID Registration

SWIDs may be registered by the Entity in a "SWID Registry", which is
managed by a "Designated Authority".

The following diagram describes the process of registering a SWID using a "SWID Registry":

![registering-a-swid-using-a-swid-registry.png](./images/registering-a-swid-using-a-swid-registry.png)

Note that registration of SWIDs in a registry is an optional step
that is separate from the creation of SWIDs. Most SWIDs will not
be recorded in a centralized registry. SWIDs may be registered in
a system of distributed, decentralized registries.

SWIDs are DIDs that can use any DID method, as long as the DIDs fulfill
the requirements in [SWIDs](#swids).

- An Entity can "bring its own SWID", which had already been created previously,
  according to the applicable DID method's [`create` function](https://identity.foundation/did-registration/#create).
- If an Entity does not yet have a SWID, the processes of creating and registering
  a SWID can be combined in a single flow. In this case, the `did:swid`
  DID method MUST be used, which has been specifically designed to meet the requirements
  of SWIDs for the Spatial Web. See [[spec: DID-SWID]] for the specification.

To register a SWID in a "SWID Registry", the [`execute` function](https://identity.foundation/did-registration/#execute) of the
DIF [[spec: DID-REGISTRATION]] specification is used.

**Example Request to register a SWID:**

```
HTTP POST to https://<swid-registry>/execute
```

```json
{
   "operation": [
      "addToRegistry"
   ],
   "operationData": [
      {}
   ],
   "did": "did:swid:zQmQoeG7u6XBtdXoek5p3aPoTjaSRemHAKrMcY2Hcjpe3jv#hstp",
   "secret": {},
   "options": {}
}
```

**Example Response:**

```json
{
    "didState": {
        "state": "finished"
    },
    "operationResult": [
        {
            "registrationConfirmation": "..."
        }
    ]
}
```

During the process of registering a SWID, the Entity MAY be required to prove control
of its SWID's associated public key, using  [Signing Requests](https://identity.foundation/did-registration/#signing-request-set)
and [Signing Responses](https://identity.foundation/did-registration/#signing-response-set).

**Example Signing Request:**

```json
{
	"jobId": "96202012-41d8-424a-85a9-3673bda6abc7",
	"didState": {
		"state": "action",
		"action": "signPayload",
		"signingRequest": {
			"signingRequestRegistration": {
				"kid": "#keys-1",
				"alg": "EdDSA",
				"purpose": "authentication",
				"serializedPayload": "<-- base 64 encoded -->"
			}
		}
	},
	"didRegistrationMetadata": { ... },
	"didDocumentMetadata": { ... }
}
```

**Example Signing Response:**

```json
{
    "jobId": "96202012-41d8-424a-85a9-3673bda6abc7",
    "options": {
        "clientSecretMode": true
    },
    "secret": {
        "signingResponse": {
            "signingRequestRegistration": {
                "signature": "<-- base64 encoded -->"
            }
        }
    },
    "didDocument": {}
}
```
