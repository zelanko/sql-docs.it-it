---
title: Questa cartella di lavoro contiene una o più query che aggiornano dati esterni | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61056ecc8b49e7d21cd15702116da511a517ef31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207999"
---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>Questa cartella di lavoro contiene una o più query che aggiornano dati esterni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Per le cartelle di lavoro di Excel contenenti dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Excel Services visualizza questo avviso quando vengono rilevate le informazioni di connessione e viene richiesto di abilitare o disabilitare le query per questa cartella di lavoro.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11_md](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]|  
|Causa|Excel Services è configurato per avvisare in caso di aggiornamento dati.|  
|Testo del messaggio|La cartella di lavoro contiene una o più query che aggiornano dati esterni. Un utente malintenzionato potrebbe creare una query per accedere a informazioni riservate e distribuirle ad altri utenti o eseguire altre azioni dannose.<br /><br /> Se la cartella di lavoro proviene da una fonte attendibile, fare clic su Sì per consentire le query su dati esterni nella cartella di lavoro. In caso contrario, fare clic su No in modo che le modifiche non vengano applicate alla cartella di lavoro.<br /><br /> Consentire le query su dati esterni nella cartella di lavoro?|  
  
## <a name="explanation"></a>Spiegazione  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] le cartelle di lavoro contengono stringhe di connessione dati incorporate utilizzate da Excel per comunicare con un server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] esterno che carica e calcola i dati. Quando l'avviso in caso di aggiornamento dati è abilitato, Excel Services rileva questa stringa di connessione e avvisa l'utente di conseguenza.  
  
 Per filtrare e sezionare i dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] nella cartella di lavoro, le query devono essere abilitate. Assicurarsi di abilitare le query solo per le cartelle di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] attendibili.  
  
## <a name="user-action"></a>Azione dell'utente  
 Fare clic su **Sì** per abilitare le query.  
  
 È anche possibile modificare le impostazioni di configurazione in modo da non ricevere più l'avviso in caso di aggiornamento:  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic su **Applicazione Excel Services**.  
  
3.  Fare clic su **Posizione attendibile file**.  
  
4.  Fare clic su **http://** o sul percorso che si desidera configurare.  
  
5.  In Dati esterni deselezionare la casella di controllo per **Avvisa in caso di aggiornamento**.  
  
6.  Fare clic su **OK**.  
  
 In alternativa, è possibile creare un nuovo percorso attendibile per i siti che contengono cartelle di lavoro di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e quindi modificare le impostazioni di configurazione solo per questo sito. Per altre informazioni, vedere [Creare un percorso attendibile per i siti PowerPivot in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  
