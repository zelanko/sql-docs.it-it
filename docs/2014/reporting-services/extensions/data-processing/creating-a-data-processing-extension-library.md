---
title: Creazione di una libreria di estensioni per l'elaborazione dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 82f4b71b-dd39-467d-8d8c-6771eb2b12de
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0c0cd3a0390fb1e7fa447264449a0bdb9407e9d1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63164350"
---
# <a name="creating-a-data-processing-extension-library"></a>Creazione di una libreria di estensioni per l'elaborazione dati
  A ogni estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] creata deve essere assegnato uno spazio dei nomi univoco e ogni estensione deve essere compilata in una libreria o in un file di assembly. Il nome esatto dello spazio dei nomi non è importante, ma è necessario che sia univoco e non condiviso con altre estensioni. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] utilizza lo spazio dei nomi <xref:Microsoft.ReportingServices.DataProcessing> per le estensioni per l'elaborazione dati disponibili in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. È necessario creare spazi dei nomi univoci personalizzati per le estensioni per l'elaborazione dati della società.  
  
 Nell'esempio seguente viene illustrato il codice per iniziare a creare un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] che utilizza gli spazi dei nomi contenenti le interfacce per l'elaborazione dati e le classi di utilità.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.DataProcessing  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.DataProcessing;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 Quando si compila un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], è necessario fornire al compilatore un riferimento a Microsoft.ReportingServices.Interfaces.dll, in quanto le interfacce dell'estensione per l'elaborazione dati sono incluse in tale elemento. Lo spazio dei nomi <xref:Microsoft.ReportingServices.DataProcessing> è necessario per implementare le interfacce dell'estensione per l'elaborazione dati, mentre lo spazio dei nomi <xref:Microsoft.ReportingServices.Interfaces> è necessario per implementare l'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IExtension>. Se, ad esempio, tutti i file che contengono il codice per implementare un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] scritti in C# fossero inclusi in una singola directory con estensione cs, da tale directory verrebbe inviato il comando seguente per compilare i file archiviati in CompanyName.ExtensionName.dll.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 L'esempio di codice seguente visualizza il comando che verrebbe usato per i file [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] con estensione vb.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll /r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  È inoltre possibile progettare, sviluppare e compilare un'estensione per l'elaborazione dati utilizzando [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Per ulteriori informazioni sullo sviluppo di assembly in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], vedere la documentazione di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Estensioni di Reporting Services](../reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
