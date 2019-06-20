---
title: Visualizzazione dei report di ottimizzazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- tuning reports [SQL Server]
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4963a309f6c54998ece968f8a5393e818fd30d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110147"
---
# <a name="viewing-tuning-reports"></a>Visualizzazione dei report di ottimizzazione
  Nell'attività precedente di questa lezione sono stati esaminati gli script [!INCLUDE[tsql](../../includes/tsql-md.md)] che consentono di creare o eliminare oggetti di database dalle indicazioni di Ottimizzazione guidata motore di database generate come risultato della sessione di ottimizzazione di MySession. La sessione di ottimizzazione di MySession è stata creata in [Ottimizzazione di un carico di lavoro](lesson-1-1-tuning-a-workload.md).  
  
 Sebbene sia molto utile visualizzare gli script che è possibile utilizzare per implementare i risultati dell'ottimizzazione, in Ottimizzazione guidata motore di database sono disponibili anche numerosi report utili. Tali report offrono informazioni sulle strutture di progettazione fisica esistenti nel database che si sta ottimizzando e sulle strutture consigliate. È possibile visualizzare i report di ottimizzazione facendo clic sulla scheda **Report** descritta nell'attività seguente. In questa attività verranno usate le sessioni di ottimizzazione di MySession ed EvaluateMySession create in [Ottimizzazione di un carico di lavoro](lesson-1-1-tuning-a-workload.md) e in [Visualizzazione delle indicazioni di ottimizzazione](lesson-1-2-viewing-tuning-recommendations.md).  
  
### <a name="view-tuning-reports"></a>Visualizzazione dei report di ottimizzazione  
  
1.  Avviare Ottimizzazione guidata motore di database. Vedere [Avvio dello strumento Ottimizzazione guidata motore di database](../../relational-databases/performance/database-engine-tuning-advisor.md). Assicurarsi di connettersi alla stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzata nell'attività precedente di questa lezione.  
  
     Nel riquadro **Monitoraggio sessione** fare doppio clic su **MySession** . Ottimizzazione guidata motore di database carica le informazioni relative a questa sessione.  
  
2.  Fare clic sulla scheda **Report** .  
  
3.  Nel riquadro **Riepilogo ottimizzazione** è possibile visualizzare le informazioni sulla sessione di ottimizzazione. Utilizzare la barra di scorrimento per visualizzare tutto il contenuto del riquadro. Si notino i valori di **Miglioramento percentuale previsto** e **Spazio utilizzato seguendo le indicazioni**. È possibile limitare lo spazio utilizzato per le indicazioni quando si impostano le opzioni di ottimizzazione. Nella scheda **Opzioni di ottimizzazione** selezionare **Opzioni avanzate**. Selezionare **Spazio massimo per le indicazioni** e specificare lo spazio massimo in megabyte che può essere usato da una configurazione consigliata. Usare il pulsante **Indietro** nel visualizzatore della Guida per tornare a questa esercitazione.  
  
4.  Nell'elenco **Selezionare il report** del riquadro **Report ottimizzazione** fare clic su **Report costo istruzioni** . Se è necessario più spazio per la visualizzazione del report, trascinare il bordo del riquadro **Monitoraggio sessione** verso sinistra. Ad ogni istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguita su una tabella del database è associato un costo delle prestazioni. Tale costo può essere ridotto creando indici efficaci sulle colonne di una tabella alle quali si accede di frequente. In questo report viene illustrato il miglioramento percentuale previsto tra il costo originale dell'esecuzione di un'istruzione del carico di lavoro e il costo previsto se viene implementata l'indicazione di ottimizzazione. Si noti che la quantità di informazioni contenute nel report dipende dalla lunghezza e dalla complessità del carico di lavoro.  
  
5.  Fare clic con il pulsante destro del mouse sul riquadro **Report costo istruzioni** nell'area della griglia e quindi scegliere **Esporta in un file**. Salvare il report come `MyReport`. L'estensione xml verrà aggiunta al nome del file automaticamente. Per visualizzare il contenuto del file MyReport.xml, è possibile aprire il report nell'editor XML preferito o in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
6.  Tornare alla scheda **Report** di Ottimizzazione guidata motore di database e fare nuovamente clic con il pulsante destro del mouse su **Report costo istruzioni** . Controllare le altre opzioni disponibili. Si noti che è possibile modificare il carattere del report visualizzato. Se la modifica del carattere avviene in questo punto, verranno modificate anche le altre pagine a schede.  
  
7.  Fare clic sugli altri report disponibili nell'elenco **Selezionare report** in modo da acquisire maggiore familiarità.  
  
## <a name="summary"></a>Riepilogo  
 A questo punto è stata esaminata la scheda **Report** dell'interfaccia utente grafica di Ottimizzazione guidata motore di database per la sessione di ottimizzazione di MySession. È possibile eseguire gli stessi passaggi per esplorare i report creati per la sessione di ottimizzazione di EvaluateMySession. Nel riquadro **Monitoraggio sessione** fare doppio clic su **EvaluateMySession** per iniziare.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: Uso dell'utilità del prompt dei comandi dta](lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
