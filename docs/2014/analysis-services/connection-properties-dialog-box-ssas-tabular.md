---
title: Finestra di dialogo Proprietà connessione (SSAS-tabulare) | Microsoft Docs
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
ms.openlocfilehash: b6e68e92658bcc32530d787630998c52e1295596
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526827"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>Finestra di dialogo Proprietà connessione (SSAS - Tabulare)
  Utilizzare questa pagina per visualizzare o modificare in SQL Server Management Studio le proprietà di connessione di un'origine dati utilizzata da un database modello tabulare.  
  
 In questa finestra di dialogo vengono forniti timestamp e altre informazioni descrittive, nonché proprietà personalizzabili che determinano le caratteristiche della connessione.  
  
## <a name="options"></a>Opzioni  
  
|Termine|Definizione|  
|----------|----------------|  
|**Nome**|Specifica il nome dell'origine dati.|  
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
  
  
