---
title: Installazione hardware - sistema di piattaforma Analitica | Microsoft Docs
description: Questo articolo descrive come spostare, decomprimere e installare i componenti hardware per l'appliance di SQL Server PDW. Questo articolo è solo informativo e può aiutare a comprendere il processo. L'appliance deve essere disimballato, installato e verificato prima viene girato all'utente. La partecipazione dei clienti è obbligatoria per gli elementi, ad esempio data center di accesso, alimentazione elettrica e connessioni Ethernet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c864a560bb37d27a5bb8ef306ac66815e8b5149c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960870"
---
# <a name="hardware-installation-for-analytics-platform-system-appliance"></a>Installazione di hardware per il dispositivo di sistema di piattaforma Analitica
Questo articolo descrive come spostare, decomprimere e installare i componenti hardware per l'appliance di SQL Server PDW. Questo articolo è solo informativo e può aiutare a comprendere il processo. L'appliance deve essere disimballato, installato e verificato prima viene girato all'utente. La partecipazione dei clienti è obbligatoria per gli elementi, ad esempio data center di accesso, alimentazione elettrica e connessioni Ethernet.  
  
## <a name="BeforeMoving"></a>Prima di spostare tutti i componenti di carico  
Eseguire le operazioni seguenti prima di spostare, decomprimere o uno qualsiasi dei componenti di appliance in rack.  
  
|Attività|Descrizione|  
|--------|---------------|  
|Verificare che tutti i componenti sono stati ricevuti|Utilizzare la distinta base (BOM) per verificare che tutti i componenti sono finalmente disponibili e sul loro palette al dock ricevente per il data center.|  
|Verificare che il data center soddisfi tutti i requisiti per l'appliance|Questa attività di avvio esaminando le specifiche hardware e cablaggio diagrammi fornendo dal fornitore IHV. I passaggi successivi forniscono i dettagli su rack i requisiti di spazio e connettività.|  
|Verificare che il data center disponga di spazio appropriata nel rack|Verificare che il data center abbia spazio sufficiente per tutti i rack appliance.<br /><br />Verificare che lo spazio di rack sia vuoto e pronto per ricevere i rack appliance.|  
|Verificare che il data center soddisfi i requisiti di connettività|Verificare che il data center soddisfi i requisiti di cablaggi nei diagrammi di cablaggio.<br /><br />Verificare che sia spazio per tutti i cavi e i cavi di alimentazione dopo che sono sia i nodi dell'appliance.|  
|Verificare che i piani tra ancoraggio e i rack soddisfino i requisiti di peso|Verificare che tutti i pavimenti tra le palette e i rack possono supportare il peso dei nodi di appliance, soprattutto nei data center con piani generati.<br /><br />Per informazioni sul peso di ogni componente, contattare il fornitore.|  
|Proteggere il data center rack|Proteggere il data center rack posto utilizzando richiedere apparecchiature aggiuntive come richiesto per la posizione del data center, ad esempio rimovibili terremoto in aree geografiche soggette a terremoti.|  
|Preparazione per ottenere assistenza con il trasporto dei componenti|Determinare in anticipo quale assistenza apparecchiature e strumenti che necessari per gestire ogni componente in modo sicuro e senza causare danni.|  
  
## <a name="Moving"></a>Spostare il rack da Dock durante il caricamento nel Data Center  
Ogni gruppo contiene tutti i componenti per rack un'appliance, inclusi i nodi, i cavi, cavi e così via.  
  
Usare l'elenco di controllo seguente per spostare ogni rack di appliance dal gruppo al dock durante il caricamento nel percorso rack nel data center. Spostare prima di tutto il rack di controllo e quindi spostare il rack di dati altre appliance.  
  
> [!WARNING]  
> Tentativo di eseguire questi passaggi esattamente come descritto può comportare danni fisiologiche, danni per l'appliance di SQL Server PDW o altri problemi.  
>   
> Non tentare mai di accuratezza o spostare un nodo di dispositivo o un altro componente pesante senza assistenza o ad apparecchiature appropriata. Contattare il fornitore IHV per informazioni sul peso di ogni componente in modo da poter determinare in anticipo quale assistenza apparecchiature e strumenti che necessari per gestire ogni componente in modo sicuro e senza causare danni.  
  
|Attività|Descrizione|  
|--------|---------------|  
|Verificare che il gruppo sia a livello di|Prima di iniziare a spostare o decomprimere il gruppo, assicurarsi che si trova in a livello zero.|  
|Unbolt un nodo di diversi|A partire dalla parte superiore del gruppo, unbolt il nodo principale dal gruppo.|  
|Spostare il nodo in un carrello della spesa in grado di supportare il peso o un carrello|Usare le rampe e tecniche di sollevare/spostamento corrette per spostare il nodo in un carrello della spesa in grado di supportare il peso o un carrello.|  
|Trasporto del nodo nel centro dati|Usare tecniche di sollevare/spostamento corrette per spostare il nodo nella posizione desiderata nel data center rack.|  
|Proteggere il nodo nel data center rack|Proteggere il nodo posto nel data center rack.|  
|Ripetere questi passaggi per il nodo o il componente successivo|Ripetere questi passaggi per spostare il nodo successivo o un altro componente appliance nel data center.|  
  
## <a name="AfterMoving"></a>Installare i componenti aggiuntivi  
Usare l'elenco di controllo seguente per installare i componenti aggiuntivi.  
  
|Attività|Descrizione||  
|--------|---------------|-|  
|Decomprimere e installare in rack PDU e switch di rete|Usare i diagrammi di rack per posizionare i commutatori di rete e PDU nella posizione appropriata nel rack.||  
|Collegare i cavi Ethernet e Infiniband, in base alle etichette di cavo|Vedere la seguente figura del cablaggio. Ogni cavo ha un'etichetta a ogni estremità che specifica dove deve essere connesso.||  
|Connettere tutti i cavi di alimentazione|Vedere la seguente figura del cablaggio.||  
|Attivare l'alimentatore per i rack e i PDU|Collegare l'alimentatore per i rack e dai rack per il PDU. **Non accendere uno qualsiasi degli altri componenti appliance in questo momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
