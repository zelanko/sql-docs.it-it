---
title: Gestito i dettagli dell'istanza (utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 6e51b7bb-a733-4852-8c33-7f4dbdf931c2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d2b01eceff763d554644065fdb5137695bd82f69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774343"
---
# <a name="managed-instance-details-sql-server-utility"></a>Dettagli di istanze gestite (Utilità SQL Server)
  Le informazioni incluse nella vista Istanze gestite di Esplora utilità forniscono dati di utilizzo per singole istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], cronologia di utilizzo della CPU, dettagli sull'utilizzo dello spazio di archiviazione a livello di file e la possibilità di visualizzare e aggiornare le soglie dei criteri. È possibile controllare le soglie dei criteri a livello di volumi di archiviazione e a livello di istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per un computer e per file di database e file di log. È inoltre possibile visualizzare dettagli delle proprietà per singole istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Visualizzazione Elenco  
 La visualizzazione Elenco nel riquadro superiore include dati relativi a singole stanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] elencate nelle righe per NomeComputer/NomeIstanza.  
  
 Le icone di stato di integrità forniscono lo stato riepilogativo per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in base alla categoria di utilizzo:  
  
-   Segno di spunta verde ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized"): numero di istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che non violano i criteri di utilizzo delle risorse. Le risorse sono utilizzate adeguatamente.  
  
-   Freccia verde rivolta verso il basso ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow"): le risorse sono sottoutilizzate.  
  
-   Freccia rossa rivolta verso l'alto ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow"): le risorse sono sovrautilizzate.  
  
 La sequenza di colonne nella visualizzazione Elenco può essere modificata trascinando le colonne verso destra o verso sinistra. È possibile aggiungere o eliminare colonne nella visualizzazione Elenco facendo clic con il pulsante destro del mouse sulle intestazioni di colonna e selezionando o deselezionando le colonne desiderate. Anche il menu di scelta rapida fornisce opzioni per l'ordinamento. È inoltre possibile attivare l'ordinamento facendo clic all'inizio di un nome di colonna.  
  
 Per accedere alle opzioni di filtro per la visualizzazione Elenco dell’utilità, fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** nel riquadro di spostamento Esplora utilità, quindi selezionare **Filtro**. Dopo l'implementazione delle impostazioni del filtro, il nodo **Istanze gestite** in Gestione Utilità verrà identificato dall'etichetta **Istanze gestite (filtrato)** . Per altre informazioni, vedere [Impostazioni filtro &#40;Esplora oggetti ed Esplora utilità&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md).  
  
 Per impostazione predefinita, nelle colonne seguenti sono visualizzate informazioni sullo stato di integrità relative a ogni istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   CPU istanza - Consente di visualizzare lo stato di integrità di utilizzo del processore allocato a questa istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   CPU computer - Consente di visualizzare lo stato di integrità di utilizzo del processore del computer. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per il computer e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   Spazio file - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo dello spazio file per tutti i database che appartengono all'istanza selezionata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se lo stato di integrità di qualsiasi database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi database è sottoutilizzato, e non sono presenti database sovrautilizzati, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Spazio volume - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo dello spazio volume per tutti i volumi che contengono database appartenenti all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]selezionata. Se lo stato di integrità di qualsiasi file di database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi volume è sottoutilizzato, e nessun volume è sovrautilizzato, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Tipo criteri - Indica se i criteri predefiniti "Globale" o i criteri personalizzati "Sostituzione" sono attivi per l'istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Altre colonne che è possibile visualizzare utilizzando il menu di scelta rapida nell'area dell'intestazione di colonna della visualizzazione Elenco:  
  
-   Nome processore:  
  
-   Velocità processore (MHz):  
  
-   Conteggio processore:  
  
-   Memoria fisica (MB):  
  
-   Versione del sistema operativo:  
  
-   Versione di SQL Server:  
  
-   Edizione di SQL Server:  
  
-   Cluster: (True o False)  
  
-   Directory di backup:  
  
-   Regole di confronto:  
  
-   Distinzione maiuscole / minuscole: (True o False)  
  
-   Lingua:  
  
-   Ora ultimo report: Questa colonna viene visualizzato il punto di controllo utilità data e ora locali utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
 Scheda Utilizzo CPU  
 La scheda Utilizzo CPU mostra grafici affiancati con dati cronologici relativi all'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e all'utilizzo della CPU del computer.  
  
 Il grafico consente di visualizzare la cronologia di utilizzo del processore per l'intervallo specificato nei pulsanti di opzione sul lato destro dell'area di visualizzazione. Per modificare l'intervallo visualizzato e aggiornare il set di dati, selezionare un pulsante di opzione dall'elenco.  
  
 Sono disponibili le opzioni di intervallo seguenti:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Scheda Utilizzo spazio di archiviazione  
 La scheda Utilizzo spazio di archiviazione include una visualizzazione albero con dettagli relativi allo spazio di archiviazione. Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
 È possibile raggruppare la visualizzazione in base al database o al volume. Per usare la visualizzazione albero del database, selezionare il pulsante di opzione **Database** nella selezione **Raggruppa file per:** . Per visualizzare lo stato di utilizzo dello spazio di archiviazione per i singoli file di database, fare clic sul segno più accanto a un nome di database nella visualizzazione albero. I file di database elencati includono tutti i sistemi e i database utente che appartengono all'istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] selezionata nella visualizzazione Elenco.  
  
 La struttura ad albero corrisponde alla gerarchia di archiviazione. Il nodo radice nella visualizzazione albero corrisponde al database. Il livello successivo della visualizzazione albero contiene un nodo o nodi filegroup che appartengono al database e un nodo del file di log per i log che appartengono al database. Il livello successivo contiene i file di dati che appartengono al filegroup.  
  
 I dati visualizzati nel grafico della cronologia di utilizzo dello spazio di archiviazione variano a seconda del nodo selezionato nella visualizzazione albero:  
  
-   Selezionare il nodo del gruppo di file per visualizzare un grafico dello spazio file utilizzato da tutti i file di dati che appartengono al gruppo di file selezionato.  
  
-   Selezionare il nodo del file di log per visualizzare un grafico dello spazio file utilizzato da tutti i file di log che appartengono al database selezionato.  
  
-   Selezionare il nodo del database per visualizzare un grafico che aggiunge lo spazio file utilizzato da tutti i file di dati e file di log che appartengono al database selezionato.  
  
 Le icone di stato di integrità forniscono informazioni immediate sullo stato di file di database, filegroup e file di log:  
  
 Per i database:  
  
-   Segno di spunta verde - Lo stato di integrità di tutti i filegroup e file di log non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo stato di integrità di almeno un filegroup o file di log è sottoutilizzato, nessuno stato di integrità è sovrautilizzato.  
  
-   Freccia in su rossa - Lo stato di integrità di almeno un filegroup o file di log è sovrautilizzato.  
  
 Per filegroup e file di log:  
  
-   Segno di spunta verde - Lo spazio file per tutti i file nel filegroup non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo spazio file per almeno un file nel filegroup è sottoutilizzato e nessun file nel filegroup è sovrautilizzato.  
  
-   Freccia in su rossa - Lo spazio file per tutti i file di dati nel filegroup è sovrautilizzato.  
  
 Per visualizzare i file in base al volume, selezionare il pulsante di opzione **Volume** nella selezione **Raggruppa file per:** . Il grafico della cronologia di utilizzo dello spazio di archiviazione consente di visualizzare lo spazio file utilizzato da tutti i file di dati e da tutti i file di log nel volume di archiviazione. Espandere l'albero per visualizzare i dettagli relativi ai singoli file di dati e file di log del database.  
  
 Le icone di stato sono utilizzate per fornire informazioni sullo stato di ogni volume:  
  
-   Segno di spunta verde - Le risorse sono utilizzate adeguatamente.  
  
-   Freccia in giù verde - Le risorse sono sottoutilizzate.  
  
-   Freccia in su rossa - Le risorse sono sovrautilizzate.  
  
 Il misuratore accanto a ogni nome file nella scheda Utilizzo spazio di archiviazione rappresenta la quantità di spazio utilizzata dal file rispetto alla capacità effettiva del file. Il valore percentuale visualizzato accanto al misuratore rappresenta la percentuale di spazio utilizzata dal file rispetto alla capacità effettiva del file. Le descrizioni comandi forniscono dati utilizzati per calcolare percentuali per ogni volume e per ogni file rispetto alla capacità effettiva.  
  
 Se il file non è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla quantità di spazio allocata per il file. Se il file è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla somma della quantità di spazio attualmente allocata per il file più la quantità di spazio libero attualmente disponibile sul volume.  
  
 È possibile configurare i criteri dello spazio di archiviazione per i file di dati e per i file di log. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per i file, fare clic sul collegamento **Criteri file** nella parte inferiore del riquadro Utilizzo spazio di archiviazione. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per un volume di archiviazione, fare clic sul collegamento **Criteri volume** nella parte inferiore del riquadro Utilizzo spazio di archiviazione.  
  
 Per sostituire le soglie di criteri predefinite, fare clic sul pulsante di opzione **Sostituisci criteri predefiniti**, specificare i valori per i limiti superiori e inferiori, quindi fare clic su **OK**.  
  
 Per altre informazioni sulla modifica di valori di tolleranza per le violazioni dei criteri, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU&#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Scheda Dettagli proprietà  
 I dettagli delle proprietà elencati per le istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] includono le categorie seguenti:  
  
-   Nome processore:  
  
-   Velocità processore (MHz):  
  
-   Conteggio processore:  
  
-   Memoria fisica (MB):  
  
-   Versione del sistema operativo:  
  
-   Versione di SQL Server:  
  
-   Edizione di SQL Server:  
  
-   Cluster: (True o False)  
  
-   Directory di backup:  
  
-   Regole di confronto:  
  
-   Distinzione maiuscole / minuscole: (True o False)  
  
-   Lingua:  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di applicazioni livello dati distribuite &#40;Utilità SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md)   
 [Dashboard utilità &#40;utilità SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Attività e funzionalità di Utilità SQL Server](../../2014/database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
