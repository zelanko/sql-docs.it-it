---
title: Selezione avanzata di oggetti (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4d2b367f-8ac7-4534-b66f-10300ef64ebc
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 42042451cb0b2197dd54270d4eca1bb990eb233d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934052"
---
# <a name="advanced-object-selection--accesstosql"></a>Selezione avanzata di oggetti (AccessToSQL)
La finestra di dialogo **sezione oggetti avanzati** consente di filtrare gli oggetti di database usando stringhe e sottostringhe nel nome dell'oggetto, quindi selezionare o deselezionare tali oggetti. SSMA esegue operazioni di conversione e migrazione sugli oggetti selezionati.  
  
Per accedere a questa finestra di dialogo, fare clic con il pulsante destro del mouse in Esplora metadati, quindi scegliere **selezione avanzata oggetti**.  
  
Quando si apre per la prima volta la finestra di dialogo, fare clic su **Mostra elementi sottocategorie** per visualizzare tutti gli oggetti i cui metadati sono stati caricati nel progetto. È quindi possibile immettere stringhe per filtrare gli elementi. Ad esempio, immettere la stringa "Company" per visualizzare tutti gli elementi con nomi che includono tale stringa.  
  
Prima di utilizzare questa finestra di dialogo, potrebbe essere necessario forzare SSMA a caricare tutti i metadati convertendo gli schemi o salvando il progetto.  
  
## <a name="options"></a>Opzioni  
**Seleziona tutti gli elementi**  
Aggiunge un segno di spunta accanto a tutti gli elementi. Questi elementi saranno selezionati immediatamente in Esplora metadati.  
  
**Deseleziona tutti gli elementi**  
Rimuove il segno di spunta accanto a tutti gli elementi. Questi elementi verranno immediatamente cancellati in Esplora metadati.  
  
**Modalità visualizzazione elenco**  
Visualizza gli elementi filtrati in un elenco.  
  
**Modalità di visualizzazione tabella**  
Visualizza gli elementi filtrati in una tabella.  
  
**Elementi caricati solo visualizzati**  
Consente di abilitare o disabilitare la visualizzazione delle categorie o degli elementi. Quando si seleziona questo pulsante, SSMA Mostra tutti gli elementi che corrispondono ai criteri di filtro e quelli caricati in precedenza. Quando questo pulsante non è selezionato, SSMA Visualizza le cartelle Category.  
  
**Filter**  
Immettere la stringa che si desidera utilizzare per filtrare gli elementi. Per trovare, ad esempio, tutti gli elementi disponibili che contengono la stringa "ID" nel nome dell'elemento, immettere la stringa "ID" nella casella **filtro** .  
  
Se gli elementi corrispondono ai criteri di filtro, le categorie o gli elementi verranno visualizzati durante la digitazione della stringa. Per visualizzare gli elementi corrispondenti, è consigliabile fare clic sul pulsante **solo elementi caricati** .  
  
**Cancella filtro**  
Cancella la casella del **filtro** .  
  
