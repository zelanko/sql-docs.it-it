---
title: Impostazione delle proprietà per il componente aggiuntivo Master Data Services per Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a041133bf26865404da6a883992176b19e837c78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479060"
---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>Impostazione delle proprietà per il componente aggiuntivo Master Data Services per Excel
  Le impostazioni del componente aggiuntivo Master Data Services per Excel determinano il modo in cui i dati vengono caricati da MDS nel componente aggiuntivo di Excel e in che modo i dati vengono pubblicati dal componente aggiuntivo per Excel in MDS.  
  
 Per creare le impostazioni per il componente aggiuntivo di Excel, aprire **Excel**, fare clic sul menu **Dati master** e quindi fare clic su **Impostazioni**. Qualsiasi utente con accesso a Excel è in grado di modificare queste impostazioni. Le impostazioni vengono applicate al computer su cui è aperto Excel.  
  
## <a name="excel-add-in-settings"></a>Impostazioni del componente aggiuntivo per Excel  
  
||||  
|-|-|-|  
|Scheda e sezione|Impostazione|Descrizione|  
|Impostazioni: Server di pubblicazione|Mostra la finestra di dialogo **Pubblicazione e annotazione** durante la pubblicazione|Selezionare questa opzione per visualizzare la finestra di dialogo **Pubblicazione e annotazione** dopo avere fatto clic su **Pubblica**e consentire di immettere una sola annotazione per tutte le modifiche o un'annotazione per ogni modifica.<br /><br /> Deselezionare questa opzione per specificare che il processo Pubblica è iniziato senza visualizzare la finestra di dialogo **Pubblicazione e annotazione** . Non si avrà la possibilità di immettere un'annotazione.|  
|Impostazioni: Versione|Selezione della versione|Selezionare la versione dei dati master che saranno caricati nel componente aggiuntivo di Excel. I possibili valori sono i seguenti:<br /><br /> **Nessuna** versione per la versione predefinita<br /><br /> **Meno** recente per impostazione predefinita sulla versione più recente più **recente per impostazione** predefinita sulla versione più recente.|  
|Impostazioni: Registrazione|Abilita registrazione dettagliata|Abilitare la registrazione per il processo di caricamento dei dati master da MDS nel componente aggiuntivo di Excel, in modo che il risultato di ogni comando nel servizio venga registrato.|  
|Impostazioni: Dimensione dell'invio in batch|Numero di celle per il caricamento|Selezionare un numero per indicare quante migliaia di celle saranno caricate in un batch caricato dal server MDS in Excel. Il valore predefinito è 50.000 celle.|  
|Impostazioni: Dimensione dell'invio in batch|Numero di celle per la pubblicazione|Selezionare un numero per indicare quante migliaia di celle saranno pubblicate in un batch restituito dal Excel al server. Il valore predefinito è 50.000 celle.|  
|Impostazioni: Server aggiunti a elenco elementi attendibili|Cancella tutto|Fare clic per cancellare l'elenco di connessioni definito come attendibile quando è stato aperto il file di query collegamento associato.|  
|Dati: Filtri|Visualizza avviso di filtro per grandi set di dati|Fare clic per mostrare un avviso se il set di dati caricato da MDS a Excel supera il numero massimo di righe o colonne.|  
|Dati: Filtri|Righe massime|Selezionare la soglia per il numero di righe da caricare, superata la quale verrà generato un avviso di filtro.|  
|Dati: Filtri|Numero massimo di colonne|Selezionare la soglia per il numero di colonne da caricare, superata la quale verrà generato un avviso di filtro.|  
|Dati: Formato cella|Modifica il colore quando i valori dell'attributo vengono modificati|Fare clic per specificare che il colore di una cella verrà modificato se si modifica il valore dell'attributo in quella cella quando si aggiorna la tabella dei componenti aggiuntivi di Excel con i nuovi dati del repository MDS.|  
|Dati: Formato cella|Modifica il colore quando i membri vengono aggiunti|Fare clic per specificare che il colore delle celle di una riga verrà modificato in caso di aggiunta di un nuovo membro alla riga durante l'aggiornamento della tabella dei componenti aggiuntivi di Excel con i nuovi dati del repository MDS.|  
  
  
