---
title: Azure AD v2 Windows Desktop aan de slag - Config | Microsoft Docs
description: Hoe een toepassing .NET Windows-bureaublad (XAML) ophalen van een toegangstoken en een API die wordt beveiligd door Azure Active Directory-v2-eindpunt niet aanroepen.
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: c42f40252733f0c4fd7fdbabb49714ea537acc70
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/01/2018
---
## <a name="add-the-applications-registration-information-to-your-app"></a>De registratiegegevens van de toepassing toevoegen aan uw app
In deze stap moet u de toepassings-Id toevoegen aan uw project.

1.  Open `App.xaml.cs` en vervang de regel die de `ClientId` met:

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a>Wat is de volgende

[!INCLUDE [Test and Validate](..\..\..\..\includes\active-directory-develop-guidedsetup-windesktop-test.md)]
