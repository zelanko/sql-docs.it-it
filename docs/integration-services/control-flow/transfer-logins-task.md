---
title: Attività Trasferisci account di accesso | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 242a5c58321ad211a7e27b28b4574433c45ceceb
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914782"
---
# <a name="transfer-logins-task"></a>Attività Trasferisci account di accesso

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Trasferisci account di accesso trasferisce uno o più account di accesso tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>Trasferimento di account di accesso tra istanze di SQL Server  
 L'attività Trasferisci account di accesso supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci account di accesso genera un evento informativo in cui è indicato il numero di account di accesso trasferiti. Genera inoltre un evento di avviso quando un account di accesso viene sovrascritto.  
  
 Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà **ExecutionValue** dell'attività, restituisce il numero di account di accesso trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà **ExecValueVariable** dell'attività, le informazioni sul trasferimento degli account di accesso possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci account di accesso include le voci di log personalizzate seguenti:  
  
-   TransferLoginsTaskStarTransferringObjects    Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferLoginsTaskFinishedTransferringObjects   Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento **OnInformation** indica il numero di account di accesso che sono stati trasferiti. Viene scritta una voce di log per l'evento **OnWarning** per ogni account di accesso sovrascritto nella destinazione.  
  
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
  
 In fase di esecuzione l'attività Trasferisci account di accesso si connette al server di origine e al server di destinazione utilizzando due gestioni di connessione SMO. Le due gestioni vengono configurate separatamente dall'attività Trasferisci account di accesso, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>Configurazione a livello di codice dell'attività Trasferisci account di accesso  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>Editor attività Trasferisci account di accesso (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività Trasferisci account di accesso** per assegnare un nome e una descrizione all'attività Trasferisci account di accesso.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per l'attività Trasferisci account di accesso. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Trasferisci account di accesso.  
  
## <a name="transfer-logins-task-editor-logins-page"></a>Editor attività Trasferisci account di accesso (pagina Account di accesso)
  Usare la pagina **Account di accesso** della finestra di dialogo **Editor attività Trasferisci account di accesso** per impostare le proprietà per la copia di uno o più account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un altra.  
  
> [!IMPORTANT]  
>  Durante l'esecuzione di questa attività, sul server di destinazione vengono creati gli account di accesso con password casuali e le password vengono disabilitate. Per usare questi account di accesso, è necessario che un membro del ruolo predefinito del server **sysadmin** cambi le password e quindi le attivi. L'account di accesso **sa** non può essere trasferito.  
  
### <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di destinazione.  
  
 **LoginsToTransfer**  
 Consente di selezionare gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da copiare dal server di origine a quello di destinazione. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**AllLogins**|Tutti gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel server di origine verranno copiati in quello di destinazione.|  
|**SelectedLogins**|Solo gli account di accesso specificati in **LoginsList** verranno copiati nel server di destinazione.|  
|**AllLoginsFromSelectedDatabases**|Tutti gli account di accesso nel database specificato in **DatabasesList** verranno copiati nel server di destinazione.|  
  
 **LoginsList**  
 Consente di selezionare gli account di accesso nel server di origine da copiare in quello di destinazione. Questa opzione è disponibile solo se è selezionata **SelectedLogins** per **LoginsToTransfer**.  
  
 **DatabasesList**  
 Consente di selezionare i database nel server di origine contenenti gli account di accesso da copiare sul server di destinazione. Questa opzione è disponibile solo se è selezionata **AllLoginsFromSelectedDatabases** per **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Consente di selezionare la modalità di gestione dei nomi già esistenti nel server di destinazione da parte dell'attività  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**FailTask**|L'attività ha esito negativo se esistono già account di accesso con lo stesso nome nel server di destinazione.|  
|**Overwrite**|L'attività sovrascrive gli account di accesso con lo stesso nome nel server di destinazione.|  
|**Skip**|L'attività ignora gli account di accesso con lo stesso nome nel server di destinazione.|  
  
 **CopySids**  
 Consente di indicare se gli identificatori di sicurezza associati agli account di accesso devono essere copiati sul server di destinazione. L'opzione**CopySids** deve essere impostata su **True** se l'attività Trasferisci account di accesso viene usata contestualmente all'attività Trasferisci database. In caso contrario, gli account di accesso copiati non verranno riconosciuti dal database trasferito.  
  
