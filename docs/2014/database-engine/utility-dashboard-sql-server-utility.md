---
title: Dashboard utilità (Utilità SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ce0c700e7e53ef1b055fa476e1e259fefe6c0aa
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/26/2020
ms.locfileid: "83857773"
---
# <a name="utility-dashboard-sql-server-utility"></a>Dashboard Utilità (Utilità SQL Server)
  Per visualizzare i dati inclusi nel dashboard Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], nell'albero Gestione Utilità selezionare il nodo principale, con l'etichetta "Utilità<Nome_PuntoDiControlloUtilità">\\(NomeComputer\PuntoDiControlloUtilità)". Il dashboard include i dati di riepilogo e i dettagli relativi a tutte le istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a tutte le applicazioni di livello dati nell'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per aggiornare dati nel dashboard, fare clic con il pulsante destro del mouse sul nodo principale nell'albero Esplora utilità e selezionare **Aggiorna**.  
  
 Per altre informazioni su come creare un punto di controllo dell'utilità, vedere [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Per altre informazioni su come aggiungere un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] all'utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 Integrità istanze gestite  
 Lo stato di integrità per le istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene visualizzato sul lato sinistro del riquadro contenuto di Esplora utilità.  
  
 I parametri relativi all'integrità dell'istanza gestita sono i seguenti:  
  
-   Utilizzo CPU per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilizzo del file di database.  
  
-   Utilizzo dello spazio del volume di archiviazione.  
  
-   Utilizzo della CPU per il computer.  
  
-   Per ogni parametro esistono le tre categorie di stato seguenti:  
  
-   Adeguatamente utilizzato - Numero di istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che non stanno violando criteri di utilizzo delle risorse.  
  
-   Sottoutilizzato - Numero di risorse gestite che stanno violando criteri di sottoutilizzo delle risorse.  
  
-   Sovrautilizzato - Numero di risorse gestite che stanno violando criteri di sovrautilizzo delle risorse.  
  
-   Dati non disponibili - I dati per le istanze gestite di SQL Server non sono disponibili perché l'istanza di SQL Server è appena stata inclusa e la prima operazione di raccolta dati non è stata completata o perché si è verificato un problema con l'istanza gestita di SQL Server durante la raccolta e il caricamento dei dati nel punto di controllo dell'utilità.  
  
 Le informazioni di stato dettagliate per ogni parametro di integrità sono elencate negli indicatori scorrevoli. La frazione a destra degli indicatori scorrevoli mostra il numero di istanze gestite incluso in ogni categoria di stato.  
  
 Per creare una visualizzazione filtrata di un'istanza gestita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o un'applicazione del livello dati, fare clic sul collegamento per una categoria di utilizzo accanto al relativo indicatore scorrevole nel dashboard dell'utilità. Ad esempio, se si fa clic su **CPU istanza sovrautilizzata** nel riquadro **Contenuto Esplora utilità** , SSMS crea una visualizzazione elenco filtrata delle istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che dispongono di una CPU sovrautilizzata in base alle impostazioni dei criteri correnti.  
  
 Si noti che quando si fa clic su un collegamento per una categoria di utilizzo, al nodo corrispondente nel riquadro di navigazione Esplora utilità viene aggiunto **(filtrato)** , ovvero **Istanze gestite** viene etichettato **Istanze gestite (filtrato)**. Per visualizzare le impostazioni del filtro, fare clic con il pulsante destro del mouse sul nodo nel riquadro di navigazione e selezionare **Filtro**, quindi fare clic su **Impostazioni filtro**. Per cancellare le impostazioni del filtro, fare clic con il pulsante destro del mouse sul nodo nel riquadro di navigazione e selezionare **Filtro**, quindi fare clic su **Rimuovi filtro**.  
  
 Per altre informazioni sulla visualizzazione dello stato di integrità per singole istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o per visualizzare o modificare impostazioni di configurazione dei criteri, vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md).  
  
 Riepilogo utilità  
 Consente di visualizzare il numero di istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e il numero di applicazioni di livello dati gestite dall'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Integrità applicazione del livello dati  
 Lo stato di integrità per le applicazioni di livello dati viene visualizzato sul lato destro del riquadro contenuto di Esplora utilità.  
  
 I parametri relativi all'integrità dell'applicazione del livello dati sono i seguenti:  
  
-   Utilizzo CPU per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilizzo del file di database.  
  
-   Utilizzo dello spazio del volume di archiviazione.  
  
-   Utilizzo della CPU per il computer.  
  
 Per ogni parametro esistono le tre categorie di stato seguenti:  
  
-   Adeguatamente utilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di utilizzo delle risorse.  
  
-   Sovrautilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di sovrautilizzo delle risorse.  
  
-   Sottoutilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di sottoutilizzo delle risorse.  
  
-   Dati non disponibili - I dati per le applicazioni di livello dati non sono disponibili perché l'istanza gestita di SQL Server che contiene l'applicazione del livello dati non sta registrando dati.  
  
 Le informazioni di stato dettagliate per ogni parametro di integrità sono elencate negli indicatori scorrevoli. La frazione a destra degli indicatori scorrevoli mostra il numero di applicazioni di livello dati incluso in ogni categoria di stato. Per altre informazioni sulla visualizzazione dello stato di integrità per le singole applicazioni di livello dati o per visualizzare o modificare le impostazioni di configurazione dei criteri, vedere [Dettagli di applicazioni di livello dati distribuite &#40;Utilità SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
 Cronologia di utilizzo dello spazio di archiviazione utilità  
 La cronologia di utilizzo viene mostrata in un grafico temporale nella parte inferiore del dashboard utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) nella documentazione online di SQL Server. Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) nella documentazione online di SQL Server.  
  
 Utilizzare i pulsanti di opzione a sinistra dell'area di visualizzazione per modificare il periodo del report per il grafico.  
  
 Le opzioni disponibili per l'intervallo del report sono:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Dopo avere apportato modifiche all'intervallo scelto per il report, i dati verranno aggiornati automaticamente.  
  
 Utilizzo di spazio di archiviazione utilità  
 Nella parte inferiore destra del dashboard, il grafico a torta relativo all'utilizzo dello spazio di archiviazione restituisce la percentuale di spazio utilizzato rispetto allo spazio disponibile nei volumi che si trovano in computer contenenti istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. I dati contenuti in questa visualizzazione vengono aggiornati ogni 15 minuti.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare Esplora utilità per gestire la Utilità SQL Server](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [Modificare una definizione dei criteri di integrità delle risorse &#40;Utilità SQL Server&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
