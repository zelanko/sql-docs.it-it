---
title: Proprietà server (pagina Connessioni) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c9d58fb2a5702a2a6c3f5ac74ae970411d887b62
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809350"
---
# <a name="server-properties-connections-page"></a>Proprietà server (pagina Connessioni)
  Utilizzare questa pagina per visualizzare o modificare le opzioni di connessione.  
  
## <a name="connections"></a>Connessioni  
 **Numero massimo di connessioni simultanee (0 = illimitato)**  
 Se questa opzione è impostata su un valore diverso da zero, limita il numero di connessioni consentite da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!CAUTION]  
>  L'impostazione di un valore basso, ad esempio 1 o 2, può impedire la connessione da parte degli amministratori ai fini dell'amministrazione del server. Tuttavia, è sempre possibile eseguire la connessione amministrativa dedicata.  
  
## <a name="default-connection-options"></a>Opzioni di connessione predefinite  
 **Default connection options**  
 Specifica le opzioni di connessione predefinite descritte nella tabella seguente.  
  
|Opzione di configurazione|Descrizione|  
|--------------------------|-----------------|  
|**disable deferred constraint checking**|Controlla la verifica dei vincoli posticipata o provvisoria.|  
|**transazioni implicite**|Determina se al momento dell'esecuzione di un'istruzione una transazione viene avviata in modo implicito.|  
|**cursor close on commit**|Determina il funzionamento dei cursori dopo l'esecuzione di un'operazione di commit.|  
|**ansi warnings**|Controlla i troncamenti e la generazione di avvisi nel caso le funzioni di aggregazione contengano valori Null.|  
|**ansi padding**|Controlla i caratteri di riempimento nelle variabili di lunghezza fissa.|  
|**ansi nulls**|Controlla la gestione dei valori `NULL` con gli operatori di uguaglianza.|  
|**arithmetic abort**|Interrompe una query quando si verifica un errore di divisione per zero o di overflow durante l'esecuzione della query stessa.|  
|**arithmetic ignore**|Restituisce un valore Null quando durante l'esecuzione di una query si verifica un errore di overflow o di divisione per zero.|  
|**quoted identifier**|Riconosce la differenza tra virgolette doppie e singole per la valutazione di un'espressione.|  
|**no count**|Disabilita la restituzione del messaggio che indica il numero di righe interessate al termine di ogni istruzione.|  
|**ansi null default on**|Modifica il funzionamento della sessione in modo che venga utilizzata la compatibilità ANSI per il supporto di valori Null. Nelle nuove colonne definite senza supporto esplicito dei valori Null sarà possibile utilizzare valori Null.|  
|**ansi null default off**|Modifica il funzionamento della sessione in modo che non venga utilizzata la compatibilità ANSI per il supporto di valori Null. Nelle nuove colonne definite senza supporto esplicito dei valori Null non sarà possibile utilizzare valori Null.|  
|**concat null yields null**|Restituisce NULL in seguito alla concatenazione di un valore Null con una stringa.|  
|**numeric round abort**|Genera un errore quando in un'espressione si verifica una perdita di precisione.|  
|**xact abort**|Esegue il rollback di una transazione se un'istruzione Transact-SQL genera un errore di run-time.|  
  
 Per ulteriori informazioni sulle opzioni di connessione, cercare l'opzione specifica sulla documentazione online.  
  
## <a name="remote-server-connections"></a>Connessioni remote  
 **Consenti connessioni remote al server**  
 Controlla l'esecuzione di stored procedure dai server remoti che eseguono istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La selezione di questa casella di controllo ha lo stesso effetto dell'impostazione dell'opzione **sp_configureremote access** su 1. La deselezione della casella di controllo impedisce l'esecuzione di stored procedure da un server remoto.  
  
 **Timeout query remote (in secondi, 0 = nessun timeout)**  
 Specifica la durata (in secondi) di un'operazione remota prima del timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore predefinito è 600 secondi, corrispondente a un'attesa di 10 minuti.  
  
 **Richiedi transazioni distribuite per le comunicazioni tra server**  
 Consente di proteggere le azioni di una procedura da server a server tramite una transazione MS DTC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator). Per altre informazioni, vedere [Configurare l'opzione di configurazione del server remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md).  
  
## <a name="property-page-display-options"></a>Opzioni di visualizzazione delle pagine delle proprietà  
 **Valori configurati**  
 Consente di visualizzare i valori configurati per le opzioni nel riquadro. Se si modificano i valori, fare clic su **Valori correnti** per verificare se le modifiche sono diventate effettive. In caso contrario, l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere prima riavviata.  
  
 **Valori correnti**  
 Consente di visualizzare i valori correnti per le opzioni contenute nel riquadro. I valori sono di sola lettura.  
  
## <a name="see-also"></a>Vedere anche  
 [Le opzioni &#40;Query in esecuzione: SQL Server: pagina avanzate&#41;](../options-query-execution-sql-server-advanced-page.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
