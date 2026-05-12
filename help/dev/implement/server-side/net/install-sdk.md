---
title: Install the .NET SDK
description: Learn how t install the [!DNL Adobe Target] .NET SDK.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
TQID: https://experienceleague.adobe.com/438ax3dEUclYIa42EvOLyBBuRngsZLHRDXabumxp0F8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Install the .NET SDK

The .NET SDK is distributed by [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). To get started, add it as a dependency by installing via `Package Manage` or `.NET CLI`:

## Package Manager

>[!BEGINTABS]

>[!TAB Package Manager]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

The open sourced code can be found at [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
