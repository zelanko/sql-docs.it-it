---
title: Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671367"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementazione di un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge
  In questo argomento viene descritto come implementare il sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)] o un [sistema di risoluzione personalizzato basato su COM](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
 **Contenuto dell'argomento**  
  
-   **Per implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge, utilizzando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Sistema di risoluzione basato su COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 È possibile scrivere un sistema di risoluzione dei conflitti personalizzato come stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] in ogni server di pubblicazione. Durante la sincronizzazione questa stored procedure viene richiamata quando vengono rilevati conflitti in un articolo per il quale il sistema di risoluzione è stato registrato e l'agente di merge passa le informazioni sulla riga con conflitti ai parametri obbligatori della procedura. I sistemi di risoluzione dei conflitti personalizzati basati su stored procedure vengono sempre creati nel server di pubblicazione.  
  
> [!NOTE]  
>  I sistemi di risoluzione delle stored procedure di[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono richiamati solo per gestire i conflitti causati da modifiche apportate alle righe. Non possono essere utilizzati per gestire altri tipi di conflitti, ad esempio errori di inserimento dovuti a violazioni di PRIMARY KEY o del vincolo di indice univoco.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>Per creare un sistema di risoluzione dei conflitti personalizzato basato su stored procedure  
  
1.  Nella pubblicazione o nel database **msdb** del server di pubblicazione creare una nuova stored procedure di sistema che implementi i parametri obbligatori seguenti:  
  
    |Parametro|Tipo di dati|Descrizione|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|Nome del proprietario della tabella per la quale risolvere un conflitto. Si tratta del proprietario della tabella nel database di pubblicazione.|  
    |**@tablename**|`sysname`|Nome della tabella per la quale risolvere un conflitto.|  
    |**@rowguid**|`uniqueidentifier`|Identificatore univoco per la riga in cui è presente il conflitto.|  
    |**@subscriber**|`sysname`|Nome del server da cui viene propagata una modifica in conflitto.|  
    |**@subscriber_db**|`sysname`|Nome del database da cui viene propagata una modifica in conflitto.|  
    |**@log_conflict OUTPUT**|`int`|Indica se il processo di merge deve registrare un conflitto da risolvere in un secondo momento:<br /><br /> **0** = Il conflitto non viene registrato.<br /><br /> **1** = La riga in conflitto è quella del Sottoscrittore.<br /><br /> **2** = La riga in conflitto è quella del server di pubblicazione.|  
    |**@conflict_message OUTPUT**|`nvarchar(512)`|Messaggio da visualizzare per la risoluzione se il conflitto viene registrato.|  
    |**@destowner**|`sysname`|Proprietario della tabella pubblicata nel Sottoscrittore.|  
  
     Questa stored procedure utilizza i valori passati dall'agente di merge a questi parametri per implementare la logica di risoluzione dei conflitti personalizzata. Deve restituire un solo set di risultati della riga la cui struttura è identica a quella della tabella di base e che contiene i valori dei dati per la versione confermata della riga.  
  
2.  Concedere autorizzazioni EXECUTE sulla stored procedure a qualsiasi account di accesso utilizzato dai Sottoscrittori per la connessione al server di pubblicazione.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un nuovo articolo di tabella  
  
1.  Eseguire [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) per definire un articolo, specificando il valore **MicrosoftSQL** **Server Stored Procedure Resolver** per il parametro **@article_resolver** e il nome della stored procedure che implementa la logica del sistema di risoluzione dei conflitti per il parametro **@resolver_info**. Per altre informazioni, vedere [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un articolo di tabella esistente  
  
1.  Eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando **@publication**, **@article**, il valore **article_resolver** per **@property** e il valore **MicrosoftSQL** **Server Stored ProcedureResolver** per **@value**.  
  
2.  Eseguire [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando **@publication**, **@article**, il valore **resolver_info** per **@property**e il nome della stored procedure che implementa la logica del sistema di risoluzione dei conflitti per **@value**.  
  
##  <a name="COM"></a> Utilizzo di un sistema di risoluzione personalizzato basato su COM  
 Lo spazio dei nomi <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa un'interfaccia che consente di scrivere logica di business complessa per gestire gli eventi e i risolvere conflitti che si verificano durante il processo di sincronizzazione della replica di tipo merge. Per altre informazioni, vedere [Implementazione di un gestore della logica di business per un articolo di merge](implement-a-business-logic-handler-for-a-merge-article.md). Per risolvere i conflitti, è inoltre possibile scrivere una logica di business personalizzata basata su codice nativo. Tale logica viene compilata come un componente COM in DLL, utilizzando prodotti quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Un simile sistema di risoluzione dei conflitti personalizzato basato su COM deve implementare l'interfaccia **ICustomResolver**, specificamente progettata per la risoluzione dei conflitti.  
  
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
  
8.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) per verificare che la libreria non sia già registrata come sistema di risoluzione dei conflitti personalizzato.  
  
9. Per registrare la libreria come sistema di risoluzione dei conflitti personalizzato, eseguire [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) nel database di distribuzione. Specificare il nome descrittivo dell'oggetto COM per **@article_resolver**, ID (CLSID della raccolta di) per **@resolver_clsid**e il valore `false` per **@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Quando un sistema di risoluzione dei conflitti personalizzato non è più necessario, è possibile annullarne la registrazione con [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql).  
  
10. (Facoltativo) In un cluster ripetere i passaggi da 5 a 8 per registrare il sistema di risoluzione personalizzato in tutti i nodi del cluster. Tale operazione è necessaria per garantire che il sistema di risoluzione personalizzato sia in grado di caricare correttamente il riconciliatore in seguito a un failover.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un nuovo articolo di tabella  
  
1.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e prendere nota del nome descrittivo del sistema di risoluzione desiderato.  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) per definire un articolo. Specificare il nome descrittivo del sistema di risoluzione dei conflitti dell'articolo ottenuto al passaggio 1 per **@article_resolver**. Per altre informazioni, vedere [definire un articolo](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Per utilizzare un sistema di risoluzione dei conflitti personalizzato con un articolo di tabella esistente  
  
1.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e prendere nota del nome descrittivo del sistema di risoluzione desiderato.  
  
2.  Eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), specificando **@publication**, **@article**, il valore **article_resolver** per **@property** e il nome descrittivo del sistema di risoluzione dei conflitti dell'articolo dal passaggio 1 per **@value**.  
  
#### <a name="viewing-a-sample-custom-resolver"></a>Visualizzazione di un sistema di risoluzione personalizzato di esempio  
  
1.  Un esempio è disponibile nei file di esempio di SQL Server 2000. Scaricare il [ **sql2000samples.zip**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip). Vengono scaricati 3 file comporta la 6,9 MB.  
  
2.  Estrarre i file dal file con estensione cab compresso scaricato.  
  
3.  Eseguire **setup.exe**  
  
    > [!NOTE]  
    >  Quando si scelgono le opzioni di installazione, è necessario installare solo gli esempi relativi alla **replica** (Il percorso di installazione predefinito è **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  Passare alla cartella di installazione. La cartella predefinita è **C:\Programmi (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**  
  
5.  Eseguire il programma **unzip_sqlreplSP3.exe** .  
  
    > [!NOTE]  
    >  Il sistema di risoluzione COM di esempio viene installato per impostazione predefinita nella cartella **C:\Programmi (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** .  
  
6.  Nella cartella **subspres** trovare tutte le occorrenze di **#include sqlres.h** in tutti i file di origine e sostituirle con **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## <a name="see-also"></a>Vedere anche  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Procedure consigliate per la sicurezza della replica](security/replication-security-best-practices.md)  
  
  
