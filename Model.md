# Data Model

In order to compare storage technologies, common data models are needed to ensure the same or at least very similar use cases are investigated.

## Model 1: Simple Asset Managment

With the simple asset management model, six distinct entity types are related to each other primarly with one-to-many and many-to-many relationships.

- Organizations
    - Data fields:
        - id: string
        - name: string
    - Can have many users
    - Can have many permissions on assets
- Users
    - Data fields:
        - id: string
        - name: string
        - email: string
        - fullname: string
        - organizationId: string
    - Can belong to several organizations
    - Can have many permissions on assets
- Permissions
    - Data fields:
        - id: string
        - type: string
    - Belongs to exactly one user or one organization
    - Belongs to exactly one asset type or asset data entry
- Asset Type
    - Data fields:
        - type: string
        - label: string
        - description: string
        - created: datetime
        - organizationId: string
        - enabled: boolean
    - Belong to exactly one organization
    - Can have many defined columns
    - Can have many data entries or instances respectively
- Asset Type Column
    - Data fields:
        - id: string
        - assetTypeId: string
        - dataType: string
        - label: string
        - description: string
    - Data types:
        - text
        - integer
        - float
        - boolean
        - datetime
        - json
    - Data type values get encoded as text
    - Belong to exactly one asset type
- Asset Data
    - Data fields:
        - id: string
        - entryId: string
        - assetTypeColumnId: string
        - value: string
    - Asset data items are grouped by the entity id because one entry is composed of the values for each data column of the asset type
    - Reference exactly one data column
    - Are thus indirectly linked to exactly one asset type

This simple model is designed to introduce some complexity by linking several entity types to each other. The model doesn't solve security aspects although it accounts for basic IAM.

The outlined entity types are not necessarily corresponding to relational database tables or collections. It depends on the storage technology how the required information models are implemented. SQL, NoSQL types as well as NewSQL storage types have their own advantages and disadvantages when it comes to representing data.