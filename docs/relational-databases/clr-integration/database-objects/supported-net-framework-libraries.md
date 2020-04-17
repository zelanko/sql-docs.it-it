---
title: Librerie .NET Framework supportate Documenti Microsoft
description: Con CLR ospitato in SQL Server, è possibile creare utilizzando le librerie di classi .NET Framework supportate e le librerie non supportate registrate con un database.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 459cd091043d567b4c93555c271213d066f3989e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487107"
---
# <a name="supported-net-framework-libraries"></a>Librerie .NET Framework supportate
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Grazie all'integrazione di CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è possibile creare stored procedure, trigger, funzioni definite dall'utente, tipi definiti dall'utente e aggregazioni definite dall'utente nel codice gestito. Con le librerie di classi .NET Framework è possibile accedere alle classi preesistenti che offrono funzionalità per manipolazione delle stringhe, operazioni matematiche avanzate, accesso ai file, crittografia e così via. A queste classi è possibile accedere da stored procedure gestite, tipi definiti dall'utente, trigger, funzioni definite dall'utente o funzioni di aggregazione definite dall'utente.  
  
> [!NOTE]  
>  Se si gestiscono o aggiornano assembly non supportati nella Global Assembly Cache (GAC), è possibile che si arresti il funzionamento dell'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ciò si verifica in quanto le operazioni di gestione o aggiornamento delle librerie presenti nella GAC non determinano l'aggiornamento degli assembly che si trovano in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se un assembly è presente sia in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sia nella GAC, le due copie relative devono corrispondere esattamente. Se non corrispondono, si verificherà un errore quando l'assembly verrà usato dalla funzionalità di integrazione con CLR di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se si esegue il servizio o l'aggiornamento di qualsiasi assembly nella Global Assembly Cache che sono anche registrati nel database, inclusi gli assembly .NET Framework non supportati, assicurarsi di servire o aggiornare anche la copia dell'assembly all'interno dei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database con l'istruzione ALTER **ASSEMBLY.** Per ulteriori informazioni, vedere [l'articolo della Knowledge Base 949080](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Librerie supportate  
 A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è disponibile un elenco di librerie .NET Framework supportate, che sono state testate per verificare che rispettino gli standard di sicurezza e di affidabilità per l'interazione con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le librerie supportate non devono essere registrate in modo esplicito nel server prima che possano essere utilizzate nel codice. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di caricarle direttamente dalla Global Assembly Cache (GAC).  
  
 Le librerie e gli spazi dei nomi supportati dall'integrazione con CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono:  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   Sistema  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>Librerie non supportate  
 Le librerie non supportate possono essere comunque chiamate da stored procedure gestite, trigger, funzioni definite dall'utente, tipi definiti dall'utente e funzioni di aggregazione definite dall'utente. La libreria non supportata deve [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] essere registrata nel database, utilizzando l'istruzione **CREATE ASSEMBLY,** prima di poter essere utilizzata nel codice. È necessario verificare e testare la sicurezza e l'affidabilità delle librerie non supportate registrate ed eseguite nel server.  
  
 Ad esempio, lo spazio dei nomi **System.DirectoryServices** non è supportato. È necessario registrare l'assembly System.DirectoryServices.dll con autorizzazioni **UNSAFE** prima di poterlo chiamare dal codice. L'autorizzazione **UNSAFE** è necessaria perché le classi nello spazio dei nomi **System.DirectoryServices** non soddisfano i requisiti per **SAFE** o **EXTERNAL_ACCESS**. Per ulteriori informazioni, vedere Restrizioni del modello di [programmazione dell'integrazione CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) e Sicurezza dall'accesso di [codice dell'integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un assieme](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Sicurezza dall'accesso di codice dell'integrazione CLRCLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrizioni relative al modello di programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
