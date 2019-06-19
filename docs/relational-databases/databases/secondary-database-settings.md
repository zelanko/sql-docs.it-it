---
title: Impostazioni database secondario | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.dest.f1
ms.assetid: f992ffc9-ee42-43fe-acec-512032f0ded1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c98f7a5714d7cd0813d5a4a7df6cf23c7b661414
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62652545"
---
# <a name="secondary-database-settings"></a>Impostazioni database secondario
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa finestra di dialogo per configurare e modificare le proprietà di un database secondario nella configurazione per il log shipping.  
  
 Per approfondimenti sui concetti correlati al log shipping, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Istanza del server secondario**  
 Visualizza il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attualmente configurata come server secondario nella configurazione per il log shipping.  
  
 **Database secondario**  
 Visualizza il nome del database secondario nella configurazione per il log shipping. Quando si aggiunge un nuovo database secondario a una configurazione per il log shipping, è possibile scegliere un database nell'elenco o digitare il nome di un nuovo database nella casella. Se si specifica direttamente il nome di un nuovo database, è necessario selezionare un'opzione nella scheda **Inizializzazione** per ripristinare un backup completo del database primario in quello secondario. Il nuovo database viene creato durante l'operazione di ripristino.  
  
 **Connect**  
 Consente di eseguire la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare come server secondario nella configurazione per il log shipping. È necessario che l'account utilizzato per la connessione sia membro del ruolo predefinito del server sysadmin nell'istanza del server secondario.  
  
 **Scheda Inizializzazione**  
 Sono disponibili le opzioni seguenti:  
  
 **Sì, genera un backup completo del database primario e ripristinalo nel database secondario**  
 Se si seleziona questa opzione, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] configura il database secondario eseguendo il backup del database primario e ripristinandolo nel server secondario. Se nella casella **Database secondario** è stato specificato il nome di un nuovo database, quest'ultimo verrà creato durante l'operazione di ripristino.  
  
 **Opzioni di ripristino**  
 Fare clic su questo pulsante se si desidera ripristinare i dati e i file di log del database secondario in percorsi diversi da quelli predefiniti nel server secondario.  
  
 Questo pulsante consente di aprire la finestra di dialogo **Opzioni di ripristino** in cui è possibile specificare i percorsi di cartelle diverse da quelle predefinite in cui si desidera che siano contenuti il database secondario e i relativi log. È necessario specificare entrambe le cartelle.  
  
 I percorsi devono fare riferimento a unità locali del server secondario e devono iniziare con una lettera di unità locale e due punti (ad esempio, `C:`). Le lettere di unità relative a connessioni di rete e i percorsi di rete non sono consentiti.  
  
 Se si fa clic sul pulsante **Opzioni di ripristino** e in seguito si decide di utilizzare le cartelle predefinite, è consigliabile annullare la finestra di dialogo **Opzioni di ripristino** . Se sono già stati specificati percorsi diversi e si decide invece di utilizzare quelli predefiniti, fare di nuovo clic su **Opzioni di ripristino** , cancellare il contenuto delle caselle di testo e quindi fare clic su OK.  
  
 **Sì, ripristina un backup esistente del database primario nel database secondario**  
 Se si seleziona questa opzione, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] utilizza un backup esistente del database primario per inizializzare il database secondario. Digitare il percorso del backup desiderato nella casella **File di backup** . Se nella casella Database secondario è stato specificato il nome di un nuovo database, quest'ultimo verrà creato durante l'operazione di ripristino.  
  
 **File di backup**  
 Se si sceglie l'opzione **Sì, ripristina un backup esistente del database primario nel database secondario**, digitare il percorso e il nome del file del backup completo del database che si desidera usare per inizializzare il database secondario.  
  
 **Opzioni di ripristino**  
 Vedere la descrizione di questo pulsante più indietro in questo argomento.  
  
 **No, il database secondario è già inizializzato**  
 Consente di specificare che il database secondario è già inizializzato e pronto ad accettare backup dei log delle transazioni del database primario. Questa opzione non è disponibile se è stato digitato il nome di un database nuovo nella casella **Database secondario** .  
  
 **Scheda Copia file**  
 Sono disponibili le opzioni seguenti:  
  
 **Cartella di destinazione per i file copiati**  
 Consente di specificare il percorso in cui devono essere copiati i backup dei log delle transazioni per il ripristino nel database secondario. Si tratta in genere di un percorso locale che fa riferimento a una cartella nel server secondario. Se la cartella si trova in un altro server, è comunque necessario specificarne il percorso UNC. L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'istanza del server secondario deve disporre delle autorizzazioni di lettura per tale cartella. È inoltre necessario concedere le autorizzazioni di lettura e scrittura per la condivisione di rete agli account proxy con cui verranno eseguiti i processi di copia e ripristino nelle istanze del server secondario. Per impostazione predefinita, si tratta dell'account del servizio SQL Server Agent dell'istanza del server secondario. I membri del ruolo sysadmin possono tuttavia scegliere altri account proxy per l'esecuzione dei processi.  
  
 **Elimina i file copiati dopo**  
 Consente di specificare per quanto tempo i file di backup dei log delle transazioni che sono stati copiati devono rimanere nella cartella di destinazione prima di essere eliminati.  
  
 **Nome processo**  
 Visualizza il nome del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent utilizzato per copiare i file di backup dei log delle transazioni dal server primario al server secondario. Al momento della prima creazione di tale processo è possibile modificarne il nome nell'apposita casella.  
  
 **Pianificazione**  
 Visualizza la pianificazione corrente del processo di SQL Server Agent utilizzato per copiare i file di backup dei log delle transazioni dal server primario a quello secondario. Fare clic su **Pianificazione**per apportarvi modifiche.  
  
 **Pianificazione**  
 Consente di modificare i parametri del processo di SQL Server Agent utilizzato per copiare i file di backup dei log delle transazioni dal server primario a quello secondario.  
  
 **Disabilita questo processo**  
 Consente di sospendere il processo di SQL Server Agent utilizzato per la copia.  
  
 **Scheda Ripristina log delle transazioni**  
 Sono disponibili le opzioni seguenti:  
  
 **Disconnetti utenti dal database per il ripristino dei backup**  
 Consente di disconnettere automaticamente gli utenti dal database secondario durante le operazioni di ripristino dei backup dei log delle transazioni.  
  
 **Modalità nessun recupero**  
 Consente di lasciare il database secondario in modalità NORECOVERY.  
  
 **Modalità standby**  
 Consente di lasciare il database secondario in modalità STANDBY. Questa modalità consente di eseguire esclusivamente operazioni di sola lettura sul database.  
  
> [!IMPORTANT]  
>  Se si modifica la modalità di recupero di un database secondario esistente, ad esempio da **Modalità nessun recupero** a **Modalità standby**, la modifica viene applicata solo dopo che il backup del log successivo è stato ripristinato nel database.  
  
 **Ritardo minimo per il ripristino dei backup**  
 Consente di scegliere l'eventuale ritardo per il ripristino dei backup dei log delle transazioni nel server secondario.  
  
 **Invia avviso se il ripristino non viene eseguito entro**  
 Consente di scegliere la quantità di tempo da attendere prima che venga generato un avviso se il ripristino dei log delle transazioni non viene eseguito.  
  
 **Nome processo**  
 Visualizza il nome del processo di SQL Server Agent utilizzato per ripristinare i backup dei log delle transazioni nel database secondario. Al momento della prima creazione di tale processo è possibile modificarne il nome nell'apposita casella.  
  
 **Pianificazione**  
 Visualizza la pianificazione corrente del processo di SQL Server Agent utilizzato per ripristinare i backup dei log delle transazioni nel database secondario. Fare clic su **Pianificazione**per apportarvi modifiche.  
  
 **Pianificazione**  
 Consente di modificare i parametri relativi al processo di SQL Server Agent utilizzato per il ripristino.  
  
 **Disabilita questo processo**  
 Consente di sospendere le operazioni di ripristino nel database secondario.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
