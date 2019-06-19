---
title: Proprietà server (pagina Impostazioni database) | Microsoft Docs
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.custom: ''
ms.date: 05/23/2019
ms.openlocfilehash: bf30a65cf0390c5b8400fe7a390520e4bdb29994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66771772"
---
# <a name="server-properties---database-settings-page"></a>Proprietà server (pagina Impostazioni database)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa pagina per visualizzare o modificare le impostazioni del database.  
  
## <a name="options"></a>Opzioni

### <a name="default-index-fill-factor"></a>Fattore di riempimento indice predefinito

Indica il livello di riempimento di ogni pagina in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando viene creato un nuovo indice utilizzando dati esistenti. Il fattore di riempimento ha effetto sulle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , in quanto la suddivisione delle pagine mano a mano che vengono riempite richiede tempo.
  
Il valore predefinito è 0. I valori validi sono compresi nell'intervallo da 0 a 100. Un fattore di riempimento 0 o 100 crea indici cluster con pagine di dati complete e indici non cluster con pagine foglia complete, ma lascia uno spazio all'interno del livello superiore dell'albero dell'indice. I valori 0 e 100 relativi al fattore di riempimento sono equivalenti.
  
Se sono impostati valori di riempimento inferiori a 100, i nuovi indici vengono creati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con pagine non completamente piene. Ogni indice occupa più spazio di archiviazione, ma lo spazio disponibile per inserimenti successivi è maggiore e non richiede suddivisioni di pagina.
  
### <a name="wait-indefinitely"></a>Attesa illimitata

Indica che non si verificherà alcun timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante l'attesa di un nuovo nastro di backup.  

### <a name="try-once"></a>Prova una sola volta

Specifica un timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se un nastro di backup non è disponibile quando necessario.

### <a name="try-for-minutes"></a>Prova per (minuti)

Specifica un timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se un nastro di backup non è disponibile entro il periodo specificato.  

### <a name="default-backup-media-retention-in-days"></a>Periodo di memorizzazione predefinito supporti di backup (giorni)

Specifica un valore predefinito valido in tutto il sistema per il periodo di memorizzazione di ogni supporto di backup dopo l'utilizzo per il backup di un database o di un log delle transazioni. Questa opzione consente di impedire la sovrascrittura dei backup per il numero di giorni indicato.  

#### <a name="compress-backup"></a>Comprimi backup

In [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] o versioni successive indica l'impostazione corrente dell'opzione **Valore predefinito di compressione backup** . Questa opzione determina l'impostazione predefinita a livello di server per la compressione di backup, come riportato di seguito:

- Se la casella **Comprimi backup** è vuota, per impostazione predefinita i nuovi backup non sono compressi.

- Se la casella **Comprimi backup** è selezionata, per impostazione predefinita i nuovi backup vengono compressi.
  
    > [!IMPORTANT]
    >  Per impostazione predefinita, la compressione aumenta significativamente l'utilizzo della CPU e la CPU aggiuntiva utilizzata dal processo di compressione può avere un impatto negativo sulle operazioni simultanee. Potrebbe pertanto essere necessario creare backup compressi con priorità bassa in una sessione in cui l'utilizzo della CPU è limitato da [Resource Governor](../../relational-databases/resource-governor/resource-governor.md). Per ulteriori informazioni, vedere [Utilizzo di Resource Governor per limitare l'utilizzo della CPU da parte della compressione dei backup &#40;Transact-SQL&#41;](../.. relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).
  
Se si è membri del ruolo predefinito del server **sysadmin** o **serveradmin**, è possibile modificare l'impostazione selezionando la casella **Comprimi backup**.  
  
Per altre informazioni, vedere [Visualizzare o configurare l'opzione di configurazione del server backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) e [Compressione backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  

#### <a name="backup-checksum"></a>Checksum di backup

Questa opzione consente di attivare o disattivare l'impostazione sp_configure per il *checksum di backup predefinito*. Questa funzionalità consente di abilitare più facilmente il checksum di backup predefinito.

### <a name="recovery-interval-minutes"></a>Intervallo di recupero (minuti)

Imposta per ogni database il numero massimo di minuti per il recupero dei database. L'impostazione predefinita è 0, che rappresenta la configurazione automatica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In pratica, questa opzione determina un tempo di recupero inferiore a un minuto e un checkpoint a intervalli di circa un minuto per i database attivi. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).  
  
### <a name="data"></a>data

Specifica il percorso predefinito dei file di dati. Fare clic sul pulsante Sfoglia per passare a un nuovo percorso predefinito. Le modifiche verranno applicate solo dopo il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="log"></a>File di log
  
Specifica il percorso predefinito dei file di log. Fare clic sul pulsante Sfoglia per passare a un nuovo percorso predefinito. Le modifiche verranno applicate solo dopo il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="configured-values"></a>Valori configurati

Consente di visualizzare i valori configurati per le opzioni nel riquadro. Se si modificano i valori, fare clic su **Valori correnti** per verificare se le modifiche sono diventate effettive. In caso contrario, l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere prima riavviata.  
  
### <a name="running-values"></a>Valori correnti

Consente di visualizzare i valori correnti per le opzioni contenute nel riquadro. I valori sono di sola lettura.  
  
## <a name="see-also"></a>Vedere anche

- [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

- [Specificare un fattore di riempimento per un indice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)