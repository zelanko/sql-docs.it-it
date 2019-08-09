---
title: Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: feee489d990bfce813c0bb16aafaf9e7e3a673cf
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661391"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementazione di un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come implementare il sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)] o un [sistema di risoluzione personalizzato basato su COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
 **Contenuto dell'articolo**  
  
-   **Per implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge, utilizzando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Sistema di risoluzione basato su COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 È possibile scrivere un sistema di risoluzione dei conflitti personalizzato come stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] in ogni server di pubblicazione. Durante la sincronizzazione questa stored procedure viene richiamata quando vengono rilevati conflitti in un articolo per il quale il sistema di risoluzione è stato registrato e l'agente di merge passa le informazioni sulla riga con conflitti ai parametri obbligatori della procedura. I sistemi di risoluzione dei conflitti personalizzati basati su stored procedure vengono sempre creati nel server di pubblicazione.  
  
> [!NOTE]  
>  I sistemi di risoluzione delle stored procedure di[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono richiamati solo per gestire i conflitti causati da modifiche apportate alle righe. Non possono essere utilizzati per gestire altri tipi di conflitti, ad esempio errori di inserimento dovuti a violazioni di PRIMARY KEY o del vincolo di indice univoco.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>Per creare un sistema di risoluzione dei conflitti personalizzato basato su stored procedure  
  
1.  Nella pubblicazione o nel database **msdb** del server di pubblicazione creare una nuova stored procedure di sistema che implementi i parametri obbligatori seguenti:  
  
    |Parametro|Tipo di dati|Descrizione|  
    |---------------|---------------|-----------------|  
    |**\@tableowner**|**sysname**|Nome del proprietario della tabella per la quale risolvere un conflitto. Si tratta del proprietario della tabella nel database di pubblicazione.|  
    |**\@tablename**|**sysname**|Nome della tabella per la quale risolvere un conflitto.|  
    |**\@rowguid**|**uniqueidentifier**|Identificatore univoco per la riga in cui è presente il conflitto.|  
    |**\@subscriber**|**sysname**|Nome del server da cui viene propagata una modifica in conflitto.|  
    |**\@subscriber_db**|**sysname**|Nome del database da cui viene propagata una modifica in conflitto.|  
    |**\@log_conflict OUTPUT**|**int**|Indica se il processo di merge deve registrare un conflitto da risolvere in un secondo momento:<br /><br /> **0** = Il conflitto non viene registrato.<br /><br /> **1** = La riga in conflitto è quella del Sottoscrittore.<br /><br /> **2** = La riga in conflitto è quella del server di pubblicazione.|  
    |**\@conflict_message OUTPUT**|**nvarchar(512)**|Messaggio da visualizzare per la risoluzione se il conflitto viene registrato.|  
    |**\@destowner**|**sysname**|Proprietario della tabella pubblicata nel Sottoscrittore.|  
  
     Questa stored procedure utilizza i valori passati dall'agente di merge a questi parametri per implementare la logica di risoluzione dei conflitti personalizzata. Deve restituire un solo set di risultati della riga la cui struttura è identica a quella della tabella di base e che contiene i valori dei dati per la versione confermata della riga.  
  
2.  Concedere autorizzazioni EXECUTE sulla stored procedure a qualsiasi account di accesso utilizzato dai Sottoscrittori per la connessione al server di pubblicazione.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un nuovo articolo di tabella  
  
1.  Eseguire [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) per definire un articolo, specificando il valore di **Sistema di risoluzione delle stored procedure** di **MicrosoftSQL** per il parametro **\@article_resolver** e il nome della stored procedure che implementa la logica del sistema di risoluzione dei conflitti per il parametro **\@resolver_info**. Per altre informazioni, vedere [definire un articolo](../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un articolo di tabella esistente  
  
1.  Eseguire [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), specificando **\@publication**, **\@article**, il valore **article_resolver** per **\@property** e il valore di **Sistema di risoluzione delle stored procedure** di **MicrosoftSQL** per **\@value**.  
  
2.  Eseguire [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), specificando **\@publication**, **\@article**, il valore **resolver_info** per **\@property** e il nome della stored procedure che implementa la logica del sistema di risoluzione dei conflitti per **\@value**.  
  
##  <a name="COM"></a> Utilizzo di un sistema di risoluzione personalizzato basato su COM  
 Lo spazio dei nomi <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa un'interfaccia che consente di scrivere logica di business complessa per gestire gli eventi e i risolvere conflitti che si verificano durante il processo di sincronizzazione della replica di tipo merge. Per altre informazioni, vedere [Implementazione di un gestore della logica di business per un articolo di merge](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). Per risolvere i conflitti, è inoltre possibile scrivere una logica di business personalizzata basata su codice nativo. Tale logica viene compilata come un componente COM in DLL, utilizzando prodotti quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Un simile sistema di risoluzione dei conflitti personalizzato basato su COM deve implementare l'interfaccia **ICustomResolver** , specificamente progettata per la risoluzione dei conflitti.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>Per creare e registrare un sistema di risoluzione dei conflitti personalizzato basato su COM  
  
1.  In un ambiente di creazione compatibile con COM aggiungere riferimenti alla libreria del sistema di risoluzione dei conflitti personalizzato.  
  
2.  Per un progetto Visual C++ utilizzare la direttiva #import per importare la libreria nel progetto.  
  
3.  Creare una classe che implementa l'interfaccia **ICustomResolver** .  
  
4.  Implementare determinati metodi e proprietà.  
  
5.  Compilare il progetto per creare il file della libreria del sistema di risoluzione dei conflitti personalizzato.  
  
6.  Distribuire la libreria nella directory che contiene il file eseguibile dell'agente di merge, in genere \Microsoft SQL Server\100\COM.  
  
    > [!NOTE]  
    >  Un sistema di risoluzione dei conflitti personalizzato deve essere distribuito nel Sottoscrittore per una sottoscrizione pull, nel server di distribuzione per una sottoscrizione push o nel server Web utilizzato con sincronizzazione tramite il Web.  
  
7.  Registrare la libreria del sistema di risoluzione dei conflitti personalizzato utilizzando regsvr32.exe nella directory di distribuzione come descritto di seguito:  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) per verificare che la libreria non sia già registrata come sistema di risoluzione dei conflitti personalizzato.  
  
9. Per registrare la libreria come sistema di risoluzione dei conflitti personalizzato, eseguire [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) nel database di distribuzione. Specificare il nome descrittivo dell'oggetto COM per **\@article_resolver**, l'ID (CLSID) della libreria per **\@resolver_clsid** e il valore **false** per **\@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Quando un sistema di risoluzione dei conflitti personalizzato non è più necessario, è possibile annullarne la registrazione con [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md).  
  
10. (Facoltativo) In un cluster ripetere i passaggi da 5 a 8 per registrare il sistema di risoluzione personalizzato in tutti i nodi del cluster. Tale operazione è necessaria per garantire che il sistema di risoluzione personalizzato sia in grado di caricare correttamente il riconciliatore in seguito a un failover.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un nuovo articolo di tabella  
  
1.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e prendere nota del nome descrittivo del sistema di risoluzione desiderato.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) per definire un articolo. Specificare il nome descrittivo del sistema di risoluzione dei conflitti dell'articolo ottenuto al passaggio 1 per **\@article_resolver**. Per altre informazioni, vedere [definire un articolo](../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un articolo di tabella esistente  
  
1.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) e prendere nota del nome descrittivo del sistema di risoluzione desiderato.  
  
2.  Eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), specificando **\@publication**, **\@article**, il valore **article_resolver** per **\@property** e il nome descrittivo del sistema di risoluzione dei conflitti dell'articolo dal passaggio 1 per **\@value**.  
  

## <a name="see-also"></a>Vedere anche  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Procedure consigliate per la sicurezza della replica](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
