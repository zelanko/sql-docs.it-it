---
title: Amministrazione utilità (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 3e5a00c3-8905-40f0-9ddc-d924df9c2f0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e67ee4d0ff2dba6edb8b9f485dc5efd903b100cf
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83857853"
---
# <a name="utility-administration-sql-server-utility"></a>Amministrazione utilità (Utilità SQL Server)
  Utilizzare le schede Amministrazione utilità per gestire le impostazioni di criteri, sicurezza e data warehouse per un'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per altre informazioni sui concetti di Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 Scheda Criteri - Utilizzare la scheda Criteri per visualizzare o specificare criteri di monitoraggio globali.  
  
 Consente di impostare i criteri di monitoraggio globali dell'applicazione del livello dati. Per espandere l'elenco dei valori disponibili per questa opzione, fare clic sulla freccia accanto al nome dei criteri o fare clic sul titolo dei criteri.  
 Se un'applicazione sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore è 0%.  
  
 Se un'applicazione sta esaurendo lo spazio file - Per modificare i criteri per l'uso dello spazio dei file di dati o file di log, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio file è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio file è 0%.  
  
 Consente di impostare i criteri di monitoraggio globali dell'applicazione istanza gestita di SQL Server. Per espandere l'elenco dei valori disponibili per questa opzione, fare clic sulla freccia accanto al nome dei criteri o fare clic sul titolo dei criteri.  
 Se un'istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore dell'istanza è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore dell'istanza è 0%.  
  
 Se un'istanza gestita di un computer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore del computer è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore del computer è 0%.  
  
 Se un'istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sta esaurendo lo spazio file - Per modificare i criteri per l'uso dello spazio dei file di dati o file di log, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio file è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio file è 0%.  
  
 Se un'un'istanza gestita di un computer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sta esaurendo lo spazio del volume di archiviazione - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio del volume del computer è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio del volume del computer è 0%.  
  
 Riduzione dei disturbi di violazione dei criteri da risorse estremamente volatili. Per espandere i controlli per questa caratteristica, fare clic sulla freccia in giù sul lato destro della visualizzazione.  
 Per ulteriori informazioni, vedere ridurre le segnalazioni non [significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 Scheda Sicurezza - Consente di visualizzare i nomi degli account di accesso con le autorizzazioni necessarie per amministrare o leggere dal punto di controllo dell'utilità.  
  
 Seleziona gli account di accesso del punto di controllo dell'utilità che verranno aggiunti al ruolo Utility Reader.  
 Il privilegio Utility Reader consente all'account utente di:  
  
-   Connettersi all'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Vedere tutti i punti di visualizzazione in Esplora utilità di SSMS.  
  
-   Vedere le impostazioni nel nodo Amministrazione utilità in Esplora utilità di SSMS.  
  
 Gli amministratori dell'utilità possono includere e rimuovere istanze di SQL Server in utilità di SQL Server e modificare criteri su istanze gestite e impostazioni di amministrazione sul punto di controllo dell'utilità.  
  
 Per essere un amministratore di utilità, è necessario avere privilegi sysadmin sull'istanza di SQL Server. Per aggiungere o modificare gli account utente per il punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], utilizzare Esplora oggetti di SSMS per aggiungere l'utente agli account di accesso al server dell'istanza punto di controllo dell'utilità di SQL Server. Per altre informazioni, vedere [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql).  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 Scheda Data warehouse - Consente di visualizzare i dettagli relativi alla configurazione per il data warehouse di gestione dell'utilità.  
  
 Conservazione dei dati  
 Specifica il periodo di mantenimento dei dati per informazioni sull'utilizzo raccolte per istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il periodo di mantenimento predefinito è di 1 anno. Il valore minimo è di 1 mese. Il valore massimo supportato è 2 anni.  
  
 Informazioni di configurazione data warehouse dell'utilità  
 Le impostazioni di configurazione seguenti non sono configurabili in questa versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Nome del data warehouse di gestione dell'utilità (UMDW): Sysutility_mdw_\<GUID>_DATA.  
  
-   Frequenza di caricamento del set di raccolta: ogni 15 minuti.  
  
 La directory dell'utilità UMDW è configurabile: \<Unità di sistema>:\Programmi\Microsoft SQL Server\MSSQL10_50.<Nome_UCP>\MSSQL\Data\\, dove \<Unità di sistema> è in genere l'unità C:\. Il file di log UMDW_\<GUID>_LOG si trova nella stessa directory.  
  
> [!NOTE]  
>  È possibile modificare la posizione del file data warehouse di gestione dell'utilità (UMDW) sysutility_mdw utilizzando i comandi collega/scollega o l'istruzione ALTER DATABASE. È consigliabile utilizzare l'istruzione ALTER DATABASE. Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
 Ritorna ai valori predefiniti  
 Per ripristinare i valori predefiniti delle impostazioni in questa scheda, fare clic sul pulsante **Ripristina impostazioni predefinite** , quindi fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Dashboard utilità &#40;Utilità SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Dettagli dell'applicazione livello dati distribuita &#40;Utilità SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Istanza gestita dettagli &#40;Utilità SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
  
