---
title: I ruoli utente per Change Data Capture Service per Oracle di attunity | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e11eea40558a8e44232eed22f08d9a60bcd7742b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394318"
---
# <a name="user-roles-for-change-data-capture-service-for-oracle-by-attunity"></a>Ruoli utente per il servizio CDC (Change Data Capture) per Oracle di Attunity
  In questa sezione sono descritti i ruoli utente per il servizio Change Data Capture per Oracle di Attunity. I ruoli descritti sono ruoli del database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ruoli di Windows o ruoli del database Oracle.  
  
## <a name="windows-user-roles"></a>Ruoli utente di Windows  
 Di seguito vengono descritti i ruoli utente di Windows utilizzati dal servizio Oracle CDC.  
  
### <a name="computer-administrator-oracle-cdc-service"></a>Amministratore del computer: servizio Oracle CDC  
 L'amministratore del computer è un utente di Windows responsabile della creazione e della gestione del servizio CDC nel computer. Deve appartenere al gruppo di amministratori del computer locale.  
  
 Tra le attività eseguite dall'amministratore del computer del servizio Oracle CDC sono incluse le seguenti:  
  
-   Installazione del servizio CDC per il software Oracle  
  
-   Creazione di un servizio di Windows Oracle CDC  
  
-   Impostazione della connessione del servizio CDC all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione (stringa di connessione e credenziali)  
  
-   Controllo della password master del servizio CDC con cui vengono protette le credenziali di log mining  
  
-   Eliminazione di un servizio di Windows del servizio CDC  
  
-   Disinstallazione del servizio CDC per il software Oracle  
  
-   Gestione del servizio CDC per il software Oracle (ad esempio installazione degli aggiornamenti)  
  
-   Avvio e arresto del servizio di Windows del servizio CDC  
  
 Nelle configurazioni di disponibilità elevata, ad esempio i cluster di failover Microsoft, l'amministratore del computer deve disporre di responsabilità e autorizzazioni aggiuntive quali:  
  
-   Installazione e manutenzione del servizio CDC per il software Oracle in tutti i nodi del cluster.  
  
-   Definizione delle risorse generiche del servizio cluster per il servizio di Windows del servizio CDC nei vari nodi del cluster.  
  
-   Funzione di amministratore del computer autorizzato come amministratore nel computer in cui è installato il servizio CDC per Oracle. Questa persona installa il servizio CDC per Oracle e utilizza la console di configurazione del servizio CDC per configurare un servizio CDC per Oracle in un computer locale.  
  
### <a name="service-account-oracle-cdc-service"></a>Account servizio: servizio Oracle CDC  
 Si tratta dell'account del servizio di Windows del servizio CDC, un account di Windows utilizzato per l'esecuzione del servizio Oracle CDC (account del servizio).  
  
 L'unico privilegio obbligatorio necessario per l'account del servizio è la possibilità di utilizzare il client Oracle e il provider ODBC del client nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo account non necessita dell'accesso ai file a meno che non sia richiesto da provider specifici, ad esempio se la stringa di connessione del client Oracle fa riferimento alle istanze del database Oracle in un file **tnsnames.ora** , nel qual caso il file deve essere accessibile in lettura all'account del servizio.  
  
 Quando si crea un servizio Oracle CDC in Windows Vista o Windows Server 2008, l'account del servizio predefinito è l'account NETWORK SERVICE.  
  
 In Windows 7, Windows Server 2008 R2 e versioni successive, l'account del servizio predefinito è Servizio NT\\<nome-servizio>.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione in un altro computer o è un'istanza cluster di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il servizio richiede la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione tramite l'autenticazione di Windows, l'account del servizio deve essere un account di dominio.  
  
## <a name="sql-server-user-roles"></a>Ruoli utente di SQL Server  
 Di seguito vengono descritti i ruoli utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzati dal servizio Oracle CDC.  
  
### <a name="oracle-cdc-service-administrator"></a>Amministratore del servizio Oracle CDC  
 L'amministratore del servizio CDC è un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con controllo completo degli artefatti del servizio Oracle CDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione. L'amministratore del servizio CDC utilizza Oracle CDC Designer Console per progettare istanze di Oracle CDC.  
  
 L'amministratore del servizio CDC deve disporre dei ruoli predefiniti del server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **public** e **dbcreator**.  
  
 Tra le attività eseguite dall'amministratore del servizio CDC sono incluse le seguenti:  
  
-   Preparazione di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ospitare istanze di Oracle CDC, che sono database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questa attività viene creato un database speciale denominato MSXDBCDC nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Creazione di un'istanza del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di Oracle CDC. L'attività include l'abilitazione del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appena creato per CDC, che richiede un amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (**sysadmin**).  
  
-   Progettazione di un'istanza di Oracle CDC. Questa attività include la specifica di informazioni relative al database Oracle di origine e alle tabelle acquisite, che richiedono un amministratore del database Oracle.  
  
-   Gestione dell'istanza di Oracle CDC nel tempo, incluse le attività di aggiunta e rimozione delle istanze di acquisizione e l'aggiornamento della configurazione.  
  
-   Abilitazione o disabilitazione di un'istanza di Oracle CDC.  
  
-   Monitoraggio dello stato di un'istanza di Oracle CDC.  
  
-   Risoluzione dei problemi che hanno effetto sull'istanza di Oracle CDC.  
  
 Il ruolo predefinito del database dell'amministratore del servizio CDC è, almeno inizialmente, **db_owner** per il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC associato all'istanza di Oracle CDC. Ciò consente all'amministratore del servizio CDC di accedere ai dati delle modifiche archiviati nel database CDC. Dopo la creazione, è possibile assegnare il ruolo **db_owner** del database CDC a un utente diverso in grado di eseguire tutte le attività elencate in precedenza, tranne la preparazione di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la creazione di un'altra istanza di Oracle CDC.  
  
 Non è necessario che l'amministratore del servizio CDC conosca la password master specificata alla creazione del servizio di Windows Oracle CDC.  
  
### <a name="system-administrator"></a>Amministratore sistema  
 L'amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un utente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui deve essere concesso il ruolo predefinito del server **sysadmin** per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associata al servizio o ai servizi Oracle CDC.  
  
 Una sola attività specifica di Oracle CDC viene eseguita dall'amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vale a dire l'abilitazione del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per un'istanza di Oracle CDC per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Questa attività viene eseguita utilizzando Oracle CDC Designer Console durante la creazione di una nuova istanza di Oracle CDC.  
  
### <a name="oracle-cdc-service-user"></a>Utente del servizio Oracle CDC  
 L'utente del servizio Oracle CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato dal servizio Oracle CDC per eseguire il lavoro in MSXDBCDC e in tutte le istanze di Oracle CDC (database CDC) gestite da questo servizio.  
  
 L'utente del servizio Oracle CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Deve essere membro dei ruoli predefiniti del database **db_dlladmin**, **db_datareader**e **db_datawriter** per tutti i database CDC gestiti dal server.  
  
-   Deve essere membro dei ruoli predefiniti del database **db_datareader** e **db_datawriter** per il database MSXDBCDC.  
  
 Poiché il servizio Oracle CDC utilizza un solo account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per tutti i database CDC e il database MSXDBCDC, è necessario eseguire il mapping di questo account di accesso in tutti questi database.  
  
### <a name="oracle-cdc-change-consumer"></a>Consumer delle modifiche Oracle CDC  
 Il consumer delle modifiche Oracle CDC è un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizza le modifiche archiviate nelle tabelle CDC nel database dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC.  
  
 Determina il ruolo utente richiesto per l'accesso a ogni tabella CDC tramite le funzioni CDC generate dall'infrastruttura di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Se non viene specificato alcun ruolo utente quando viene specificata un'istanza di acquisizione, l'accesso alle modifiche è limitato al membro del ruolo predefinito del database **db_owner** del database CDC.  
  
## <a name="oracle-user-roles"></a>Ruoli utente di Oracle  
 Di seguito vengono descritti i ruoli utente di Oracle utilizzati dal servizio Oracle CDC.  
  
### <a name="database-administrator-dba"></a>Amministratore del database  
 L'amministratore del database Oracle è un utente del database Oracle. Tra le attività eseguite dall'amministratore del database Oracle sono incluse le seguenti:  
  
-   Impostazione del database Oracle di origine per l'utilizzo in modalità ARCHIVELOG.  
  
-   Impostazione di un utente di log mining con le autorizzazioni necessarie.  
  
-   Impostazione della registrazione supplementare per le tabelle acquisite.  
  
-   Assistenza nel ripristino dei file di log delle transazioni archiviati che non sono più disponibili per consentirne l'elaborazione.  
  
 L'amministratore del database Oracle può ottenere script Oracle SQL da eseguire in modo da poterli valutare prima dell'esecuzione. L'amministratore del database Oracle può inoltre eseguire direttamente script Oracle SQL da Oracle CDC Designer Console.  
  
 Se l'amministratore del database Oracle sceglie di usare Oracle CDC Designer Console, le credenziali di amministratore non vengono mantenute a eccezione del contesto (finestra di dialogo) in cui vengono usate.  
  
 L'amministratore del database Oracle collabora con l'amministratore del servizio Oracle CDC alla configurazione delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC.  
  
### <a name="log-mining-user"></a>Utente di log mining  
 L'utente di log mining Oracle è un utente speciale del database Oracle cui vengono concessi i privilegi necessari per l'accesso e l'elaborazione dei log delle transazioni Oracle.  
  
 Le credenziali per questo utente vengono archiviate nel database dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC mediante la crittografia a chiavi asimmetriche. Sono accessibili solo al servizio Oracle CDC, ma non al proprietario del database dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC.  
  
 Nell'elenco seguente vengono descritti i privilegi che è necessario concedere all'utente di log mining:  
  
-   SELECT on \<qualsiasi-tabella-acquisita>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE on DBMS_LOGMNR  
  
-   SELECT on V$LOGMNR_CONTENTS  
  
-   SELECT on V$ARCHIVED_LOG  
  
-   SELECT on V$LOG  
  
-   SELECT on V$LOGFILE  
  
-   SELECT on V$DATABASE  
  
-   SELECT on V$THREAD  
  
-   SELECT on V$PARAMETER  
  
-   SELECT on DBA_REGISTRY  
  
-   SELECT on ALL_INDEXES  
  
-   SELECT on ALL_OBJECTS  
  
-   SELECT on DBA_OBJECTS  
  
-   SELECT on ALL_TABLES  
  
 Se non è possibile concedere alcuni di questi privilegi a un V$xxx, è necessario concederli a V_$xxx.  
  
### <a name="schema-user"></a>Utente dello schema  
 L'utente dello schema Oracle dispone di accesso in lettura allo schema delle tabelle Oracle da acquisire. Si tratta di un utente necessario quando si utilizza Oracle CDC Designer Console per recuperare l'elenco dello schema Oracle, tabelle da acquisire con colonne, indici e chiavi associati.  
  
 Le credenziali per questo utente non vengono mai archiviate. Sono richieste da CDC Designer Console ogni volta che sono necessarie e vengono conservate per la durata delle sessioni dell'interfaccia utente.  
  
  
