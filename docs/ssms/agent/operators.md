---
title: Operatori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8d7aef10ba6a593217b4bba1c2cb984b8074b77a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65088960"
---
# <a name="operators"></a>Operatori
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Gli operatori sono alias per persone o gruppi che possono ricevere notifiche elettroniche a completamento dei processi o quando vengono generati avvisi. Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent supporta il servizio di notifica degli amministratori tramite gli operatori. Gli operatori consentono di abilitare la notifica e le funzionalità di monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="operator-attributes-and-concepts"></a>Attributi e concetti relativi agli operatori  
Gli attributi principali di un operatore sono i seguenti:  
  
-   Nome operatore  
  
-   Informazioni sul contatto  
  
### <a name="naming-an-operator"></a>Denominazione di un operatore  
A ogni operatore deve essere assegnato un nome. I nomi degli operatori devono essere univoci nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non possono essere formati da più di **128** caratteri.  
  
### <a name="contact-information"></a>Informazioni sul contatto  
Le informazioni sul contatto di un operatore definiscono la modalità di trasmissione delle notifiche all'operatore. Gli operatori possono ricevere notifiche tramite posta elettronica o cercapersone oppure tramite il comando **Net Send** :  
  
> [!IMPORTANT]
> Le opzioni Cercapersone e **net send** verranno rimosse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare pertanto di utilizzarle in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui sono state implementate.  
  
-   **Notifica tramite posta elettronica**  
  
    La notifica tramite posta elettronica prevede l'invio di un messaggio di posta elettronica all'operatore. Per la notifica tramite posta elettronica, è necessario specificare l'indirizzo di posta elettronica dell'operatore.  
  
-   **Notifica tramite cercapersone**  
  
    I messaggi vengono inviati al cercapersone tramite la posta elettronica. Per la notifica tramite cercapersone, è necessario specificare l'indirizzo di posta elettronica in cui l'operatore riceve i messaggi del cercapersone. Per configurare la notifica tramite cercapersone, è necessario installare nel server di posta un prodotto software che elabori i messaggi di posta in arrivo e li converta in messaggi per cercapersone. Il software può operare in diversi modi, tra cui quelli indicati di seguito:  
  
    -   Inoltro della posta a un server di posta remoto nel sito del provider del cercapersone.  
  
        È necessario che il provider del cercapersone offra questo servizio, anche se il software necessario fa in genere parte del sistema di posta elettronica locale. Per ulteriori informazioni, vedere la documentazione del cercapersone.  
  
    -   Routing della posta tramite Internet a un server di posta elettronica appartenente al sito del provider del cercapersone.  
  
        Si tratta di una variante della modalità descritta in precedenza.  
  
    -   Elaborazione della posta in arrivo e composizione del numero del cercapersone tramite un modem collegato.  
  
        Il prodotto software è di proprietà del provider del servizio cercapersone. Il software funziona come client di posta elettronica che elabora periodicamente la posta in arrivo, interpretando una parte dell'indirizzo del messaggio di posta o l'intero indirizzo come numero di cercapersone oppure trovando la corrispondenza tra l'indirizzo di posta elettronica e un numero di cercapersone in una tabella di conversione.  
  
        Se tutti gli operatori utilizzano lo stesso provider di cercapersone, è possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per specificare l'eventuale formattazione speciale richiesta dal sistema di comunicazione tra il cercapersone e la posta elettronica. La formattazione speciale può essere costituita da un prefisso o da un suffisso e inserita nelle righe seguenti del messaggio di posta elettronica:  
  
        **Subject:**  
  
        **Cc**:  
  
        **A**:  
  
    > [!NOTE]  
    > Se si utilizza un sistema di cercapersone alfanumerico a capacità limitata, è possibile ridurre il numero di caratteri escludendo dalla notifica su cercapersone il testo del messaggio di errore. Vi sono, ad esempio, sistemi di cercapersone alfanumerici con un limite di 64 caratteri per chiamata.  
  
-   **notifica Net Send**  
  
    Questa modalità prevede l'invio all'operatore di un messaggio tramite il comando **Net Send** . Per la notifica tramite comando **Net Send**, è necessario specificare il destinatario, costituito da un computer o un utente, di un messaggio di rete.  
  
    > [!NOTE]  
    > Il comando **Net Send** prevede l'uso di Microsoft Windows Messenger. Per consentire il corretto invio degli avvisi, il servizio deve essere in esecuzione sia nel computer in cui è in esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che in quello utilizzato dall'operatore.  
  
## <a name="alerting-and-fail-safe-operators"></a>Invio di notifiche degli avvisi agli operatori e operatori alternativi  
È possibile selezionare gli operatori che dovranno ricevere le notifiche in risposta a un avviso. Si possono ad esempio assegnare a rotazione le responsabilità degli operatori tramite la pianificazione degli avvisi. Ad esempio, la persona A riceverà notifiche degli avvisi generati lunedì, mercoledì o venerdì, mentre la persona B riceverà notifiche degli avvisi generati martedì, giovedì e sabato.  
  
L'operatore alternativo riceve una notifica relativa a un avviso quando nessuna delle notifiche agli operatori designati tramite cercapersone è riuscita. Se, ad esempio, sono stati definiti tre operatori per le notifiche tramite cercapersone e nessuno di questi operatori è raggiungibile, verrà trasmessa una notifica all'operatore alternativo.  
  
L'operatore alternativo riceve una notifica nei casi seguenti:  
  
-   Gli operatori ai quali è destinato l'avviso non sono raggiungibili.  
  
    L'impossibilità di raggiungere tali operatori potrebbe essere dovuta a un errore negli indirizzi dei cercapersone o al fatto che gli operatori non sono in servizio.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è in grado di accedere alle tabelle di sistema nel database **msdb** .  
  
    La tabella di sistema **sysnotifications** specifica le responsabilità degli operatori per i vari tipi di avvisi.  
  
L'operatore alternativo rappresenta una funzionalità di sicurezza. Per questo motivo, non è possibile eliminare l'operatore assegnato a tale compito se non dopo avere riassegnato l'incarico a un altro operatore o avere eliminato completamente l'assegnazione.  
  
## <a name="notifying-an-operator"></a>Invio di una notifica a un operatore  
Per inviare una notifica a un operatore, è necessario configurare una o più impostazioni tra le seguenti:  
  
-   Per inviare messaggi di posta elettronica tramite la funzionalità Posta elettronica database, è necessario disporre di accesso a un server di posta che supporti SMTP.  
  
-   Per inviare messaggi su cercapersone, è necessario disporre di componenti hardware e/o software di terze parti per il collegamento tra il cercapersone e la posta elettronica.  
  
-   Per usare il comando **Net Send**, l'operatore deve essere connesso al computer specificato e il computer specificato deve consentire la ricezione di messaggi da Windows Messenger.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Attività**|**Argomento**|  
|Attività correlate alla creazione di un operatore|[Creazione di un operatore](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|Attività correlate all'assegnazione di avvisi|[Assegnazione di avvisi a un operatore](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[Definizione della risposta a un avviso &#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[Assegnazione di avvisi a un operatore](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>Vedere anche  
[Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
