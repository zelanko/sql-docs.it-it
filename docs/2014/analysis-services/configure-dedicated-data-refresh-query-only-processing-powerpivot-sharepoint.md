---
title: Configurare l'aggiornamento dati dedicata o l'elaborazione di sole Query (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5e027605-1086-4941-bb01-f315df8f829b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c3b42834bc12048680c97465810832f5431441d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680435"
---
# <a name="configure-dedicated-data-refresh-or-query-only-processing-powerpivot-for-sharepoint"></a>Configurare l'aggiornamento dati o l'elaborazione di sole query dedicato (PowerPivot per SharePoint)
  Nella modalità integrata SharePoint, è possibile configurare un'istanza del server Analysis Services per supportare un tipo specifico di richiesta di elaborazione, ad esempio l'aggiornamento dei dati o l'elaborazione di sole query. Per impostazione predefinita, sono abilitati entrambi i tipi di richieste di caricamento. È possibile disabilitare uno dei due tipi per creare un motore di query o un server di aggiornamento dei dati dedicato.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  In questa versione non sono presenti impostazioni di configurazione per limitare l'utilizzo della memoria o della CPU per i processi di aggiornamento dei dati o le query su richiesta. In un'istanza del [!INCLUDE[ssGeminiSrv](../includes/ssgeminisrv-md.md)] saranno utilizzate tutte le risorse disponibili per eseguire le query e i processi di aggiornamento dei dati in corso di gestione.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Configurare una modalità di elaborazione](#config)  
  
 [Modificare il numero di processi di aggiornamento dati eseguibili in parallelo](#change)  
  
##  <a name="config"></a> Configurare una modalità di elaborazione  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci servizi nel server**.  
  
2.  In Server, nella parte superiore della pagina, fare clic sulla freccia giù, quindi scegliere **Cambia server**.  
  
3.  Selezionare il server SharePoint che dispone dell'istanza del server Analysis Services che si desidera configurare.  
  
4.  Scegliere **SQL Server Analysis Services**.  
  
5.  In Utilizzo istanza del servizio eseguire una delle operazioni seguenti:  
  
    1.  Deselezionare la casella di controllo **Abilita il caricamento dei database di sola lettura** per disattivare l'elaborazione di query su richiesta che si verifica ogni volta che un utente apre una cartella di lavoro contenente dati PowerPivot.  
  
    2.  Deselezionare la casella di controllo **Abilita il caricamento di database per l'aggiornamento** per disattivare l'aggiornamento dati pianificato.  
  
    > [!NOTE]  
    >  La disabilitazione dell'aggiornamento dei dati non comporta la rimozione delle opzioni di aggiornamento dei dati dai siti di SharePoint. Gli utenti che possiedono cartelle di lavoro PowerPivot possono ancora creare pianificazioni per l'aggiornamento dei dati, tuttavia quest'ultimo non si verificherà in tale server.  
  
6.  Facoltativamente, per le operazioni di aggiornamento dei dati, è possibile modificare il numero di processi di aggiornamento simultanei. L'aumento del numero di processi simultanei viene consigliato se il server è configurato solo per l'aggiornamento dei dati o se nel server sono presenti processori aggiuntivi. È possibile ridurre il numero di processi simultanei se si desidera liberare risorse di sistema per più query su richiesta.  
  
7.  Salvare le modifiche. Il server non consentirà di convalidare le voci finché non si verifica un evento di elaborazione. Se si immette un numero non valido per i processi simultanei, l'errore sarà rilevato e registrato quando viene elaborata la richiesta successiva.  
  
##  <a name="change"></a> Modificare il numero di processi di aggiornamento dati eseguibili in parallelo  
 Un processo di aggiornamento dei dati è un'attività pianificata aggiunta a una coda di elaborazione gestita e monitorata da un'applicazione di servizio PowerPivot. Un processo è costituito da informazioni sulla pianificazione per una o più origini dati in una cartella di lavoro PowerPivot. Un processo separato viene creato per ogni pianificazione definita. Se un proprietario della cartella di lavoro definisce una pianificazione per tutte le origini dati, sarà creato un solo processo per tutta l'operazione di aggiornamento dei dati. Se un proprietario della cartella di lavoro crea singole pianificazioni per le origini dati esterne, verranno creati più processi, i quali saranno eseguiti per effettuare un aggiornamento dei dati completo per tale cartella di lavoro.  
  
 È possibile aumentare il numero di processi di aggiornamento dei dati che possono essere eseguiti contemporaneamente se il sistema dispone della capacità di supportare il carico aggiuntivo.  
  
|Impostazione|Valori validi|Descrizione|  
|-------------|------------------|-----------------|  
|Valore predefinito|Calcolati in base alla RAM.|Il valore predefinito si basa sulla quantità di memoria disponibile divisa per 4 gigabyte. L'impostazione predefinita viene calcolata tramite una formula in modo che le impostazioni possano essere regolate a seconda delle funzionalità del sistema.<br /><br /> Nota: La divisione per 4 gigabyte è stata selezionata in base all'utilizzo di RAM per un grande campione di origini dati PowerPivot effettive. Non si basa sull'architettura fisica o logica di PowerPivot.|  
|Valore massimo|Calcolati in base al numero di CPU.|Il numero massimo di processi simultanei che è possibile specificare è basato sul numero di processori del computer. Ad esempio, in un computer quad-core a 4 socket, il numero massimo di processi che è possibile eseguire contemporaneamente è 16.|  
  
#### <a name="increasing-the-default-value-to-a-higher-value"></a>Aumento del valore predefinito a un valore superiore  
 Nel grafico seguente vengono illustrate combinazioni diverse di RAM e CPU e vengono indicati i valori massimi e predefiniti calcolati in base alle caratteristiche del sistema. Si ricordi che il valore predefinito calcolato per il numero di processi di aggiornamento dati eseguibili simultaneamente è basato sulla memoria di sistema, mentre il valore massimo calcolato è basato sulla CPU. L'ultima colonna indica se è possibile aumentare il numero massimo di processi di aggiornamento dati simultanei.  
  
|RAM effettiva (in gigabyte)|Valore predefinito calcolato|Numero effettivo di CPU|Valore massimo calcolato|Possibilità di aumentare i processi simultanei|  
|---------------------------------|------------------------------|------------------------|------------------------------|-------------------------------|  
|4|1|1|1|No. I valori massimi e predefiniti si equivalgono.|  
|4|1|4|4|Sì. È possibile aumentare il numero di processi simultanei a 2, 3 o 4.|  
|8|2|4|4|Sì. È possibile aumentare il numero di processi simultanei a 3 o 4.|  
|16|4|4|4|No. I valori massimi e predefiniti si equivalgono.|  
|32|Utilizzando la formula per il calcolo del valore predefinito, il valore predefinito sarebbe 8. Poiché il valore predefinito è maggiore del valore massimo consentito, il valore predefinito calcolato non viene utilizzato in questo caso.|4|4|No. Anche se la RAM grande indicherebbe un'impostazione predefinita di 8 processi simultanei, in un computer che dispone di 4 processori saranno supportati solo un massimo di 4 processi simultanei.|  
|32|8|8|8|No.|  
|32|8|16|16|Sì.|  
|64|16|16|16|No.|  
  
 Poiché non si può sapere in anticipo se è possibile eseguire contemporaneamente più processi in modo corretto, è necessario aumentare il numero di processi simultanei solo dopo aver analizzato il consumo di memoria nel tempo e stabilito che la memoria del server è generalmente sottoutilizzata.  
  
 Ogni processo di aggiornamento dei dati disporrà di caratteristiche di caricamento diverse a seconda del numero e delle dimensioni delle origini dati aggiornate. Il carico di elaborazione delle cartelle di lavoro che dispongono di una sola origine dati con un numero più piccolo di righe è molto più leggero rispetto a quello di una cartella di lavoro che dispone di numerose origini dati e di set di righe molto grandi.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dati PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
