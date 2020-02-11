---
title: Attività Trasferisci account di accesso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 805c89c24b0a16051de1d555b484a0870de0cfde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62830012"
---
# <a name="transfer-logins-task"></a>Attività Trasferisci account di accesso
  L'attività Trasferisci account di accesso trasferisce uno o più account di accesso tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Trasferimento di account di accesso tra istanze di SQL Server  
 L'attività Trasferisci account di accesso supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci account di accesso genera un evento informativo in cui è indicato il numero di account di accesso trasferiti. Genera inoltre un evento di avviso quando un account di accesso viene sovrascritto.  
  
 Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà `ExecutionValue` dell'attività, restituisce il numero di account di accesso trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà `ExecValueVariable` dell'attività, le informazioni sul trasferimento degli account di accesso possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci account di accesso include le voci di log personalizzate seguenti:  
  
-   TransferLoginsTaskStarTransferringObjects    Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferLoginsTaskFinishedTransferringObjects   Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento `OnInformation` indica il numero di account di accesso che sono stati trasferiti e viene scritta una voce di log per l'evento `OnWarning` per ogni account di accesso sovrascritto nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 Per poter esplorare gli account di accesso nel server di origine e creare account di accesso nel server di destinazione, è necessario che l'utente sia un membro del ruolo del server sysadmin in entrambi i server.  
  
## <a name="configuration-of-the-transfer-logins-task"></a>Configurazione dell'attività Trasferisci account di accesso  
 È possibile configurare l'attività per il trasferimento di tutti gli account di accesso, degli account di accesso specificati o di tutti gli account di accesso che accedono ai database specificati. L'account di accesso sa non può essere trasferito. È possibile rinominare l'account di accesso sa. Dopo essere stato rinominato, tuttavia, l'account di accesso sa non può essere trasferito.  
  
 È inoltre possibile specificare se l'attività deve copiare gli identificatori di sicurezza (SID) associati agli account di accesso. Se l'attività Trasferisci account di accesso viene utilizzata insieme all'attività Trasferisci database, i SID devono essere copiati nella destinazione. Se non si esegue questa operazione, gli account di accesso trasferiti non vengono riconosciuti dal database di destinazione.  
  
 Nella destinazione gli account di accesso trasferiti vengono disabilitati e vi vengono assegnate password casuali. Un membro del ruolo sysadmin nel server di destinazione deve modificare le password e attivare gli account di accesso in modo che possano essere utilizzati.  
  
 Gli account di accesso da trasferire potrebbero essere già presenti nella destinazione. È possibile configurare l'attività Trasferisci account di accesso per la gestione degli account di accesso duplicati nei modi seguenti:  
  
-   Gli account di accesso duplicati vengono sovrascritti.  
  
-   In presenza di account di accesso duplicati l'attività ha esito negativo.  
  
-   Gli account di accesso duplicati vengono ignorati.  
  
 In fase di esecuzione l'attività Trasferisci account di accesso si connette al server di origine e al server di destinazione utilizzando due gestioni di connessione SMO. Le due gestioni vengono configurate separatamente dall'attività Trasferisci account di accesso, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Trasferisci account di accesso &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Trasferisci account di accesso &#40;pagina Account di accesso&#41;](../transfer-logins-task-editor-logins-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configurazione a livello di codice dell'attività Trasferisci account di accesso  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  
