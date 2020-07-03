---
title: Librerie di .NET Framework supportate | Microsoft Docs
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
ms.openlocfilehash: 5365af51625bb528743590e9e4077ec75c40527e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885934"
---
# <a name="supported-net-framework-libraries"></a>Librerie .NET Framework supportate
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Grazie all'integrazione di CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è possibile creare stored procedure, trigger, funzioni definite dall'utente, tipi definiti dall'utente e aggregazioni definite dall'utente nel codice gestito. Con le librerie di classi .NET Framework è possibile accedere alle classi preesistenti che offrono funzionalità per manipolazione delle stringhe, operazioni matematiche avanzate, accesso ai file, crittografia e così via. A queste classi è possibile accedere da stored procedure gestite, tipi definiti dall'utente, trigger, funzioni definite dall'utente o funzioni di aggregazione definite dall'utente.  
  
> [!NOTE]  
>  Se si gestiscono o aggiornano assembly non supportati nella Global Assembly Cache (GAC), è possibile che si arresti il funzionamento dell'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ciò si verifica in quanto le operazioni di gestione o aggiornamento delle librerie presenti nella GAC non determinano l'aggiornamento degli assembly che si trovano in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se un assembly è presente sia in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sia nella GAC, le due copie relative devono corrispondere esattamente. Se non corrispondono, si verificherà un errore quando l'assembly verrà usato dalla funzionalità di integrazione con CLR di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se si esegue il servizio o si aggiornano assembly nella GAC che sono registrati anche nel database, inclusi gli assembly di .NET Framework non supportati, assicurarsi di eseguire anche il servizio o aggiornare la copia dell'assembly all'interno dei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database con l'istruzione **ALTER assembly** . Per ulteriori informazioni, vedere l' [articolo della Knowledge Base 949080](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Librerie supportate  
 A partire da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è disponibile un elenco di librerie .NET Framework supportate, che sono state testate per verificare che rispettino gli standard di sicurezza e di affidabilità per l'interazione con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le librerie supportate non devono essere registrate in modo esplicito nel server prima che possano essere utilizzate nel codice. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di caricarle direttamente dalla Global Assembly Cache (GAC).  
  
 Le librerie e gli spazi dei nomi supportati dall'integrazione con CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono:  
  
-   CustomMarshalers  
-   Microsoft.VisualBasic  
-   Microsoft.VisualC  
-   mscorlib  
-   System  
-   System.Configuration  
-   System.Core  
-   System.Data  
-   System.Data.OracleClient  
-   System.Data.SqlXml  
-   System.Deployment  
-   System.Security  
-   System.Transactions  
-   System.Web.Services  
-   System.Xml  
-   System.Xml.Linq  

<!--
Any modifications to the list above should be duplicated on the following page:
https://docs.microsoft.com/sql/relational-databases/clr-integration/assemblies-designing#supported-net-framework-assemblies
-->

## <a name="unsupported-libraries"></a>Librerie non supportate  
 Le librerie non supportate possono essere comunque chiamate da stored procedure gestite, trigger, funzioni definite dall'utente, tipi definiti dall'utente e funzioni di aggregazione definite dall'utente. La libreria non supportata deve prima essere registrata nel [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database, utilizzando l'istruzione **create assembly** , prima di poterla utilizzare nel codice. È necessario verificare e testare la sicurezza e l'affidabilità delle librerie non supportate registrate ed eseguite nel server.  
  
 Lo spazio dei nomi **System. DirectoryServices** , ad esempio, non è supportato. È necessario registrare l'assembly System.DirectoryServices.dll con autorizzazioni non **sicure** prima che sia possibile chiamarlo dal codice. L'autorizzazione **unsafe** è necessaria perché le classi nello spazio dei nomi **System. DirectoryServices** non soddisfano i requisiti per **Safe** o **EXTERNAL_ACCESS**. Per altre informazioni, vedere [restrizioni del modello di programmazione dell'integrazione CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) e [sicurezza dall'accesso di codice per l'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Sicurezza dall'accesso di codice per l'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrizioni relative al modello di programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
