---
title: Uso di assembly personalizzati con nome sicuro | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 31479ae9b460b6a660ec865e68e46afd912f49b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194083"
---
# <a name="using-strong-named-custom-assemblies"></a>Utilizzo di assembly personalizzati con nome sicuro
  Un nome sicuro identifica un assembly e include il nome di testo dell'assembly, il numero di versione in quattro parti, informazioni sulle impostazioni cultura (se disponibili), una chiave pubblica e una firma digitale archiviata nel manifesto dell'assembly. Un nome sicuro identifica in modo univoco un assembly in CLR (Common Language Runtime) e assicura l'integrità binaria.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>Utilizzo di AllowPartiallyTrustedCallersAttribute  
 Per usare assembly con nome sicuro con i report, è necessario consentire la chiamata a tali assembly da un codice parzialmente attendibile usando l'attributo **AllowPartiallyTrustedCallers** dell'assembly. È possibile usare **AllowPartiallyTrustedCallersAttribute** per consentire la chiamata agli assembly con nome sicuro da Progettazione report o dal server di report nelle espressioni di report. Per consentire al codice parzialmente attendibile di chiamare gli assembly con nome sicuro, aggiungere l'attributo a livello di assembly seguente al file di attributo dell'assembly.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** è efficace solo quando viene applicato da un assembly con nome sicuro a livello di assembly. Per altre informazioni sull'applicazione degli attributi a livello di assembly, vedere Applicazione di attributi nella documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!CAUTION]  
>  Quando è presente **AllowPartiallyTrustedCallersAttribute**, i controlli di sicurezza **FullTrustLinkDemand** predefiniti non vengono eseguiti, per rendere possibile la chiamata all'assembly da qualsiasi altro assembly parzialmente attendibile. Tutti i controlli di sicurezza, inclusi gli attributi di sicurezza dichiarativi a livello di classe o di metodo, devono essere dichiarati in modo esplicito.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di assembly personalizzati con i report](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
