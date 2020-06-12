---
title: La cartella di lavoro contiene una o più query che aggiornano dati esterni. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6e13b648b35cb0a6b6d9272ec9a2b9d560c3c7f4
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547743"
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>La cartella di lavoro contiene una o più query che aggiornano dati esterni.
  Per le cartelle di lavoro di Excel contenenti dati PowerPivot, in Excel Services viene visualizzato questo avviso quando vengono rilevate le informazioni di connessione e viene richiesto di abilitare o disabilitare le query per questa cartella di lavoro.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Excel Services è configurato per avvisare in caso di aggiornamento dati.|  
|Testo del messaggio|La cartella di lavoro contiene una o più query che aggiornano dati esterni. Un utente malintenzionato potrebbe creare una query per accedere a informazioni riservate e distribuirle ad altri utenti o eseguire altre azioni dannose.<br /><br /> Se la cartella di lavoro proviene da una fonte attendibile, fare clic su Sì per consentire le query su dati esterni nella cartella di lavoro. In caso contrario, fare clic su No in modo che le modifiche non vengano applicate alla cartella di lavoro.<br /><br /> Consentire le query su dati esterni nella cartella di lavoro?|  
  
## <a name="explanation"></a>Spiegazione  
 Le cartelle di lavoro di PowerPivot contengono stringhe di connessione dati incorporate utilizzate da Excel per comunicare con un server PowerPivot esterno che carica e calcola i dati. Quando l'avviso in caso di aggiornamento dati è abilitato, Excel Services rileva questa stringa di connessione e avvisa l'utente di conseguenza.  
  
 Per filtrare e sezionare i dati PowerPivot nella cartella di lavoro, le query devono essere abilitate. Assicurarsi di abilitare le query solo per le cartelle di lavoro di PowerPivot attendibili.  
  
## <a name="user-action"></a>Azione dell'utente  
 Fare clic su **Sì** per abilitare le query.  
  
 È anche possibile modificare le impostazioni di configurazione in modo da non ricevere più l'avviso in caso di aggiornamento:  
  
1.  In Gestione applicazioni di amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic su **Applicazione Excel Services**.  
  
3.  Fare clic su **Posizione attendibile file**.  
  
4.  Fare clic su **http://** o sul percorso che si vuole configurare.  
  
5.  In Dati esterni deselezionare la casella di controllo per **Avvisa in caso di aggiornamento**.  
  
6.  Fare clic su **OK**.  
  
 In alternativa, è possibile creare un nuovo percorso attendibile per i siti che contengono cartelle di lavoro di PowerPivot, quindi modificare le impostazioni di configurazione solo per questo sito. Per altre informazioni, vedere [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
