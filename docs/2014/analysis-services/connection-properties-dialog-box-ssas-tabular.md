---
title: Finestra di dialogo Proprietà connessione (SSAS - tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26fa80cc770d4bee9163ec18c21b35bd8c807bde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086987"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>Finestra di dialogo Proprietà connessione (SSAS - Tabulare)
  Utilizzare questa pagina per visualizzare o modificare in SQL Server Management Studio le proprietà di connessione di un'origine dati utilizzata da un database modello tabulare.  
  
 In questa finestra di dialogo vengono forniti timestamp e altre informazioni descrittive, nonché proprietà personalizzabili che determinano le caratteristiche della connessione.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Name**|Specifica il nome dell'origine dati.|  
|**ID**|Visualizza l'identificatore dell'oggetto origine dati.|  
|**Descrizione**|Visualizza la descrizione dell'oggetto origine dati.|  
|**Timestamp creazione**|Consente di visualizzare la data e l'ora di creazione del database.|  
|**Ultimo aggiornamento schema**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento dei metadati del database.|  
|**Stringa di connessione**|Visualizza la stringa di connessione utilizzata per stabilire una connessione all'origine dati che fornisce dati al modello.|  
|**Numero massimo di connessioni**|Specifica il numero massimo di connessioni client a questo database.|  
|**Isolamento**|I valori validi sono ReadCommitted o Snapshot. Per altre informazioni, vedere [Elemento Isolation &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl).|  
|**Timeout query**|Specifica il tempo, in secondi, dopo il quale si verifica il timeout del tentativo di recuperare i dati.|  
|**Provider gestito**|Specifica il nome del provider gestito. Se la connessione all'origine dati utilizza un provider OLE DB nativo, questo valore è vuoto.|  
|**Impostazioni di rappresentazione**|Viene specificato l'account di rappresentazione utilizzato per le connessioni al database quando vengono elaborati o aggiornati i dati, le query eseguite su un archivio dati relazionale (tramite DirectQuery), le associazioni out-of-line, le partizioni remote e la sincronizzazione del database dalla destinazione all'origine.<br /><br /> I valori validi includono l'account del servizio Analysis Services o un set specifico di credenziali di Windows. Non specificare **Usa credenziali dell'utente corrente** o **Eredita**. Tali opzioni per le credenziali non sono supportate per un database modello tabulare.|  
  
  
