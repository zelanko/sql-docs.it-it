---
title: Anteprima tabella selezionata (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0f168dabd237fe685eb90d2caeeba0db4eed97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070716"
---
# <a name="preview-selected-table-ssas"></a>Anteprima tabella selezionata (SSAS)
  Questa pagina dell' **Importazione guidata tabella** consente di visualizzare in anteprima i dati nella tabella selezionata, selezionare le colonne da includere nell'importazione dei dati e filtrare i dati nelle colonne selezionate. Per accedere alla procedura guidata da [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], dal menu **Modello** selezionare **Importa da origine dati**.  
  
 Non vengono visualizzate tutte le righe della tabella. Tuttavia, i filtri impostati verranno applicati a tutti i dati presenti nella tabella durante l'importazione.  
  
 Per origini dati in cui viene utilizzata l'autenticazione di Windows, le credenziali dell'utente corrente vengono utilizzate per recuperare i dati visualizzati nella finestra di dialogo Visualizza anteprima e applica filtro. Per altre origini dati, vengono utilizzate le credenziali fornite nella stringa di connessione per il recupero dei dati.  
  
 L'aspetto dei dati in questa pagina non garantisce che l'importazione verrà completata. Se il nome utente specificato nella pagina Impostazioni di rappresentazione non dispone di privilegi sufficienti per leggere dal database selezionato, l'importazione non verrà completata.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Casella di controllo nell'intestazione di colonna**  
 Selezionare la casella di controllo per includere la colonna nell'importazione dei dati. Deselezionare la casella di controllo per rimuovere la colonna dall'importazione dei dati.  
  
 **Pulsante freccia in giù nell'intestazione di colonna**  
 Consente di filtrare i dati nella colonna.  
  
 **Cancella filtri di riga**  
 Consente di rimuovere tutti i filtri applicati ai dati nelle colonne.  
  
  
