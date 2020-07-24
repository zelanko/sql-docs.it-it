---
title: Installazione hardware
description: Questo articolo descrive come spostare, decomprimere e installare l'hardware per il dispositivo SQL Server PDW. Questo articolo è esclusivamente informativo e può essere utile per comprendere il processo. Il dispositivo deve essere decompresso, installato e verificato prima che venga riattivato. La partecipazione dei clienti è necessaria per elementi quali l'accesso data center, l'alimentazione elettrica e le connessioni Ethernet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2e6a0d89b4976076f14fe567b7a95e7cbb47c9f9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942333"
---
# <a name="hardware-installation-for-analytics-platform-system-aps-appliance"></a>Installazione dell'hardware per il dispositivo Analytics Platform System (APS)
Questo articolo descrive come spostare, decomprimere e installare l'hardware per il dispositivo SQL Server PDW. Questo articolo è esclusivamente informativo e può essere utile per comprendere il processo. Il dispositivo deve essere decompresso, installato e verificato prima che venga riattivato. La partecipazione dei clienti è necessaria per elementi quali l'accesso data center, l'alimentazione elettrica e le connessioni Ethernet.  
  
## <a name="before-you-move-any-components-from-the-loading-dock"></a><a name="BeforeMoving"></a>Prima di spostare i componenti dal Dock di caricamento  
Prima di spostare, decomprimere o rack i componenti dell'appliance, eseguire le attività seguenti.  
  
|Attività|Descrizione|  
|--------|---------------|  
|Verificare che tutti i componenti siano arrivati|Usare la distinta base (BOM) per verificare che tutti i componenti siano arrivati e che si trovino sui pallet nel Dock di ricezione per la data center.|  
|Verificare che il data center soddisfi tutti i requisiti per l'appliance|Per avviare questa attività, esaminare le specifiche hardware e i diagrammi di cablaggio fornite da IHV. Nei passaggi successivi vengono fornite informazioni specifiche su spazio rack e requisiti di connettività.|  
|Verificare che il data center disponga dello spazio rack appropriato|Verificare che il data center disponga di spazio sufficiente per tutti i rack dell'appliance.<br /><br />Verificare che lo spazio del rack sia vuoto e pronto per ricevere i rack dell'appliance.|  
|Verificare che il data center soddisfi i requisiti di connettività|Verificare che il data center soddisfi i requisiti di cablaggio nei diagrammi di cablaggio.<br /><br />Verificare che sia disponibile spazio per tutti i cavi e i cavi di alimentazione dopo il rack dei nodi del dispositivo.|  
|Verificare che i piani tra il Dock e i rack soddisfino i requisiti di peso|Verificare che tutte le pavimentazioni tra i pallet e i rack siano in grado di supportare il peso dei nodi dell'appliance, soprattutto nei data center con piani sollevati.<br /><br />Per informazioni sul peso di ogni componente, contattare il IHV.|  
|Proteggere il rack data center|Proteggere il rack data center sul posto usando apparecchiature aggiuntive, come richiesto per la data center posizione, ad esempio cinghie sismiche in aree geografiche soggette a terremoti.|  
|Preparare l'assistenza per il trasporto dei componenti|Determinare in anticipo l'assistenza, le attrezzature e gli strumenti necessari per gestire ogni componente in modo sicuro e senza causare danni.|  
  
## <a name="move-the-racks-from-the-loading-dock-into-the-data-center"></a><a name="Moving"></a>Spostare i rack dal Dock di caricamento nel Data Center  
Ogni pallet contiene tutti i componenti per un rack Appliance, inclusi nodi, cavi, cavi e così via.  
  
Usare il seguente elenco di controllo per spostare ogni rack dell'appliance dal pallet sul dock di caricamento alla posizione del rack nel data center. Spostare prima il rack di controllo, quindi spostare gli altri rack di dati dell'appliance.  
  
> [!WARNING]  
> L'impossibilità di eseguire questi passaggi esattamente come descritto potrebbe causare danni fisici, danni al dispositivo SQL Server PDW o ad altri problemi.  
>   
> Non tentare mai di sollevare o spostare un nodo del dispositivo o un altro componente pesante senza assistenza o apparecchiature appropriate. Contattare il IHV per informazioni sul peso di ogni componente, in modo da poter determinare in anticipo quali sono gli strumenti, le attrezzature e gli strumenti necessari per gestire ogni componente in modo sicuro e senza causare danni.  
  
|Attività|Descrizione|  
|--------|---------------|  
|Verificare che il pallet sia a livello|Prima di iniziare a spostare o decomprimere il pallet, assicurarsi che sia a livello di piano.|  
|Disbolt di un nodo dal pallet|Iniziando dalla parte superiore del pallet, disbolt il primo nodo dal pallet.|  
|Spostare il nodo in un dolly o un carrello in grado di supportare il peso|Usare le rampe e le tecniche di sollevamento/spostamento appropriate per spostare il nodo in un dolly o un carrello in grado di supportare il peso.|  
|Trasporto del nodo nel data center|Usare le tecniche di sollevamento/spostamento appropriate per spostare il nodo nella posizione del rack data center.|  
|Proteggere il nodo nella data center rack|Proteggere il nodo sul posto nel rack data center.|  
|Ripetere questi passaggi per il nodo o il componente successivo|Ripetere questi passaggi per spostare il nodo successivo o un altro componente dell'appliance nel data center.|  
  
## <a name="install-additional-components"></a><a name="AfterMoving"></a>Installare componenti aggiuntivi  
Utilizzare l'elenco di controllo seguente per installare i componenti aggiuntivi.  
  
|Attività|Descrizione|
|--------|---------------|
|Decomprimere e commutatori di rete rack e PDU|Usare i diagrammi rack per inserire i commutatori di rete e PDU nella posizione corretta nel rack.|
|Connettere i cavi Infiniband e Ethernet in base alle etichette dei cavi|Vedere il diagramma di cablaggio. Ogni cavo ha un'etichetta a ogni estremità che specifica il punto in cui deve essere connessa.|
|Connetti tutti i cavi di alimentazione|Vedere il diagramma di cablaggio.|
|Accendere l'alimentatore per i rack e il PDU|Connettere l'alimentatore ai rack e dai rack alla PDU. **Non accendere gli altri componenti del dispositivo in questo momento.**|
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
