---
title: Distribuito i dettagli dell'applicazione livello dati (utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.dac.details.F1
helpviewer_keywords:
- utility, management
- Utility
- SQL Server Utility [SQL Server]
- data-tier application [SQL Server], utility details
- Multi-server management [SQL Server]
ms.assetid: 79c41dd9-abcb-434e-9326-00a341d5c867
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ca9186b93e96c60e1c5128e385b5b77d5f2b94e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354919"
---
# <a name="deployed-data-tier-application-details-sql-server-utility"></a>Dettagli delle applicazioni livello dati distribuite (Utilità SQL Server)
  Le informazioni incluse nella vista Applicazioni livello dati distribuite di Gestione Utilità forniscono dati di utilizzo relativi a singole applicazioni livello dati, cronologia dell'utilizzo della CPU, dettagli sull'utilizzo dello spazio di archiviazione a livello di file e la possibilità di visualizzare e aggiornare le soglie dei criteri. È possibile controllare le soglie dei criteri a livello di applicazione del livello dati per utilizzo della CPU, file di database e file di log. È inoltre possibile visualizzare dettagli delle proprietà per le singole applicazioni di livello dati.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Visualizzazione Elenco  
 La visualizzazione Elenco nel riquadro superiore include dati sulle singole applicazioni di livello dati. Le icone di stato di integrità forniscono lo stato riepilogativo per ogni applicazione del livello dati in base alle categorie di utilizzo:  
  
-   Segno di spunta verde ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized"): numero di applicazioni livello dati che non violano i criteri di utilizzo delle risorse. Le risorse sono utilizzate adeguatamente.  
  
-   Freccia verde rivolta verso il basso ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow"): le risorse sono sottoutilizzate.  
  
-   Freccia rossa rivolta verso l'alto ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow"): le risorse sono sovrautilizzate.  
  
 La sequenza di colonne nella visualizzazione Elenco può essere modificata trascinando le colonne verso destra o verso sinistra. È possibile aggiungere o eliminare colonne nella visualizzazione Elenco facendo clic con il pulsante destro del mouse sulle intestazioni di colonna e selezionando o deselezionando le colonne desiderate. Anche il menu di scelta rapida fornisce opzioni per l'ordinamento. È inoltre possibile attivare l'ordinamento facendo clic all'inizio di un nome di colonna.  
  
 Per accedere alle opzioni di filtro per la visualizzazione Elenco di Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , fare clic con il pulsante destro del mouse sul nodo **Applicazioni livello dati distribuite** nel riquadro di spostamento Esplora utilità e selezionare **Filtro**. Dopo l'implementazione delle impostazioni di filtro, il nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in Esplora utilità sarà identificato dall'etichetta **Deployed Data-tier Applications (filtered)**(Applicazioni livello dati distribuite - con filtro). Per altre informazioni, vedere [Impostazioni filtro &#40;Esplora oggetti ed Esplora utilità&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md).  
  
 Per impostazione predefinita, nelle colonne seguenti sono visualizzate informazioni sullo stato di integrità relative a ogni applicazione del livello dati.  
  
-   Nome - Nome dell'applicazione del livello dati.  
  
-   CPU applicazione - Consente di visualizzare lo stato di integrità di utilizzo del processore per questa applicazione del livello dati. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per l'applicazione del livello dati e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa applicazione livello dati o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   CPU computer - Consente di visualizzare lo stato di integrità di utilizzo del processore del computer. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per il computer e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa applicazione livello dati o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   Spazio file - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo spazio file per ogni applicazione del livello dati.  
  
    -   Segno di spunta verde - Lo stato di integrità per tutti i filegroup e il gruppo file di log non è né sovrautilizzato né sottoutilizzato.  
  
    -   Freccia in giù verde - Lo stato di integrità di almeno un filegroup o gruppo file di log è sottoutilizzato, nessun filegroup o gruppo di file di log è sovrautilizzato.  
  
    -   Freccia in su rossa - Lo stato di integrità di almeno un filegroup o il gruppo file di log è sovrautilizzato. Si noti che se il database si trova in stato di "emergenza", lo stato di integrità visualizzerà lo spazio sovrautilizzato del file di log.  
  
     Per visualizzare o modificare i limiti dei criteri di spazio per i file, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Spazio volume - Consente di visualizzare un riepilogo di stati di integrità di utilizzo dello spazio volume per tutti i volumi che contengono database appartenenti all'applicazione del livello di dati selezionata. Se lo stato di integrità di qualsiasi file di database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi volume è sottoutilizzato, e nessun volume è sovrautilizzato, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Tipo criteri - Indica se i criteri predefiniti "Globale" o i criteri personalizzati "Sostituzione" sono attivi per l'applicazione del livello di dati.  
  
-   Nome istanza - Consente di visualizzare il nome dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che ospita l'applicazione del livello di dati.  
  
 Altre colonne che è possibile visualizzare utilizzando il menu di scelta rapida nell'area dell'intestazione di colonna della visualizzazione Elenco:  
  
-   Nome database  
  
-   Data di distribuzione  
  
-   Trustworthy: (True o False)  
  
-   Confronto  
  
-   Livello di compatibilità: (ad esempio Versione100)  
  
-   Crittografia abilitata: (True o False)  
  
-   Modello di recupero: (Semplice, completo o con registrazione minima delle operazioni Bulk)  
  
-   Ora ultimo report: Questa colonna viene visualizzato il punto di controllo utilità data e ora locali utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
 Scheda Utilizzo CPU  
 La scheda Utilizzo CPU mostra grafici affiancati con dati cronologici relativi all'applicazione del livello dati e all'utilizzo della CPU del computer.  
  
 Il grafico consente di visualizzare la cronologia di utilizzo del processore per l'intervallo specificato nei pulsanti di opzione sul lato destro dell'area di visualizzazione. Per modificare l'intervallo visualizzato e aggiornare il set di dati, selezionare un pulsante di opzione dall'elenco.  
  
 Sono disponibili le opzioni di intervallo seguenti:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Scheda Utilizzo spazio di archiviazione  
 La scheda Utilizzo spazio di archiviazione include una visualizzazione albero con i dettagli relativi all'utilizzo dello spazio di archiviazione per file di database e file di log che appartengono all'applicazione del livello dati selezionata nella visualizzazione Elenco. Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
 È possibile raggruppare la visualizzazione in base al filegroup o al volume. Per utilizzare la visualizzazione albero filegroup, selezionare il pulsante di opzione **Filegroup** nella selezione **Raggruppa file per:** .  
  
 I dati visualizzati nel grafico della cronologia di utilizzo dello spazio di archiviazione variano a seconda del nodo selezionato nella visualizzazione albero:  
  
-   Selezionare il nodo del gruppo di file per visualizzare un grafico dello spazio file utilizzato da tutti i file di dati che appartengono al gruppo di file selezionato.  
  
-   Selezionare il nodo del file di log per visualizzare un grafico dello spazio file utilizzato da tutti i file di log che appartengono al database selezionato.  
  
-   Selezionare il nodo del database per visualizzare un grafico che aggiunge lo spazio file utilizzato da tutti i file di dati e file di log che appartengono al database selezionato.  
  
 Per visualizzare lo stato di utilizzo dello spazio di archiviazione per i singoli file, fare clic sul segno più accanto a un nome di file nella visualizzazione albero.  
  
 Le icone di stato di integrità forniscono informazioni immediate sullo stato di ogni filegroup rispetto alle soglie dei criteri:  
  
-   Segno di spunta verde - Lo spazio file per almeno un file di dati nel filegroup non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo spazio file per almeno un file di dati nel filegroup è sottoutilizzato e nessun file nel filegroup è sovrautilizzato.  
  
-   Freccia in su rossa - Lo spazio file per tutti i file di dati nel filegroup è sovrautilizzato. Si noti che se il database si trova in stato di "emergenza", lo stato di integrità visualizzerà lo spazio sovrautilizzato del file di log.  
  
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
 I dettagli delle proprietà elencati per le applicazioni del livello dati includono le categorie seguenti:  
  
-   Nome database  
  
-   Data di distribuzione  
  
-   Trustworthy: (True o False)  
  
-   Confronto  
  
-   Livello di compatibilità: (ad esempio Versione100)  
  
-   Crittografia abilitata: (True o False)  
  
-   Modello di recupero: (Semplice, completo o con registrazione minima delle operazioni Bulk)  
  
-   Ora ultimo report: Questa colonna viene visualizzato il punto di controllo utilità data e ora locali utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Dashboard utilità &#40;utilità SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
