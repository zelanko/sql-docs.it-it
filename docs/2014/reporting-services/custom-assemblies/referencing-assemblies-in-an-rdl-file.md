---
title: Riferimento agli assembly in un file RDL| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc52419f382ea44fc718a47e99bbd0981275d240
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63264800"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Impostazione di un riferimento agli assembly in un file RDL
  Per supportare l'uso di assembly di codice personalizzati nei file di definizione report, nella specifica RDL (Report Definition Language) sono inclusi due elementi RDL, ovvero l'elemento **CodeModules** e l'elemento **Classes**.  
  
 L'elemento **CodeModules** consente di fare riferimento agli assembly di codice gestito nelle espressioni di report. **CodeModules** è un elemento di livello principale che contiene il riferimento all'assembly usato nei file di definizione report per chiamare funzioni specializzate. Una voce in una definizione del report che supporta l'utilizzo di un assembly personalizzato può essere simile alla seguente:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 Anziché chiamare <xref:System.Reflection.Assembly.Load%2A> dal codice personalizzato, registrare gli assembly personalizzati aggiungendo manualmente elementi **CodeModule** al file RDL o usando la scheda **Riferimenti** della finestra di dialogo **Proprietà report**. Per altre informazioni, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)sottostante.  
  
 L'elemento **Classes** supporta l'uso di membri di istanza in una definizione del report. **Classes** è un elemento di livello principale che contiene un riferimento al nome della classe e un nome dell'istanza. Una voce in una definizione del report che supporta l'utilizzo di membri dell'istanza può essere simile alla seguente:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Per altre informazioni, vedere [Accesso agli assembly personalizzati tramite espressioni](accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Utilizzo di assembly personalizzati con i report](using-custom-assemblies-with-reports.md)  
  
  
