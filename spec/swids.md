## SWIDs

A Spatial Web Identifier (SWID) is any DID which fulfills the following two requirements:

1. The DID and its associated DID document MUST be conformant to the [[spec: DID-CORE]]
specification.

2. The associated DID document MUST be a conformant [SWID document](#swid-document), i.e. it MUST have at least
one [HSTP Service Endpoint](#hstp-service-endpoint-type) and MAY have more than one.

There is no direct restriction for SWIDs with regard to which DID method they use, as long as the two requirements
above are fulfilled. Different DID methods have different properties with regard to decentralization, scalability,
cost, etc. Depending on the use case, some DID methods may be more suited than others due to such properties.

Note that some DID methods have technical limitations that make them unsuitable for SWIDs. For example, the
`did:key` DID method does not support service endpoints in DID document, therefore this DID method cannot be used
for SWIDs.

Note that one DID method - `did:swid` - has been specifically designed to meet the requirements
of SWIDs for the Spatial Web. See [[spec: did-swid-spec]] for the specification.
