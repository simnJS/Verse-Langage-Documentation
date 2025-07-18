
```verse
BasicShapes := module:
cube<public> := class<final><public>(mesh_component):

    sphere<public> := class<final><public>(mesh_component):

    plane<public> := class<final><public>(mesh_component):

    cone<public> := class<final><public>(mesh_component):

    cylinder<public> := class<final><public>(mesh_component):
WebAPI<public> := module:

```
    # Usage:
    #     Licensed users create a derived version of `client_id` in their module.
    #     The Verse class path for your derived `client_id` is then used as the 
    #     configuration key in your backend service to map to your endpoint.
    # 
    #     WARNING: do not make your derived `client_id` class public. This object
    #     type is your private key to your backend.
    # 
    # Example:
    #     my_client_id<internal> := class<final><computes>(client_id)
    #     MyClient<internal> := MakeClient(my_client_id)

```verse
    client_id<native><public> := class<abstract><computes>:

    client<native><public> := class<final><computes><internal>:
        Get<native><public>(Path:string)<suspends>:response

    response<native><public> := class<internal>:

    body_response<native><public> := class<internal>(response):
        GetBody<native><public>()<computes>:string

    MakeClient<constructor><native><public>(ClientId:client_id)<converges>:client

JSON<public> := module:
    value<native><public> := class:

```
        # Retrieve an object value or fail if value is not a json object

```verse
        AsObject<native><public>()<transacts><decides>:[string]value


```
        # Retrieve an array value or fail if value is not a json array

```verse
        AsArray<native><public>()<transacts><decides>:[]value


```
        # Retrieve an integer value or fail if value is not a json number

```verse
        AsInt<native><public>()<transacts><decides>:int


```
        # Retrieve a float value or fail if value is not a json number

```verse
        AsFloat<native><public>()<transacts><decides>:float


```
        # Retrieve an object value or fail if value is not a string

```verse
        AsString<native><public>()<transacts><decides>:string


```
        # Retrieve an object value or fail if value is not null

```verse
        AsNull<native><public>()<transacts><decides>:void


```
    # Parse a JSON string returning a value with its contents

```verse
    Parse<native><public>(JSONString:string)<transacts><decides>:value

using {/UnrealEngine.com/Temporary/SpatialMath}
using {/Verse.org/Assets}


```
