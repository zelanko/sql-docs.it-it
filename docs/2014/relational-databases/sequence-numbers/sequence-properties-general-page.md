---
title: Proprietà sequenza (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 846e7960e9aca4bfb5deea8f50eae3c8a2f58c70
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184424"
---
# <a name="sequence-properties-general-page"></a>Proprietà sequenza (pagina Generale)
  Crea un oggetto sequenza e ne specifica le proprietà. Una sequenza è un oggetto associato a schema definito dall'utente che genera una sequenza di valori numerici in base alla specifica con la quale è stata creata la sequenza. La sequenza di valori numerici viene generata in ordine crescente o decrescente a un intervallo definito e può essere configurata per riprendere dall'inizio (ciclo) quando è esaurita. Le sequenze, a differenza delle colonne Identity, non sono associate a tabelle specifiche. Le applicazioni fanno riferimento a un oggetto sequenza per recuperare il relativo valore successivo. La relazione tra sequenze e tabelle è controllata dall'applicazione. Le applicazioni utente possono fare riferimento a un oggetto sequenza e coordinare i valori di più righe e tabelle.  
  
 A differenza dei valori delle colonne Identity, generati al momento dell'inserimento, un'applicazione può ottenere il numero di sequenza successivo senza inserire la riga chiamando la [funzione NEXT VALUE FOR](/sql/t-sql/functions/next-value-for-transact-sql). Usare [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) per ottenere immediatamente più numeri di sequenza.  
  
 Per informazioni e scenari in cui vengono usate entrambe le funzioni **CREATE SEQUENCE** e **NEXT VALUE FOR** , vedere [Numeri di sequenza](sequence-numbers.md).  
  
 È possibile accedere a questa pagina in due modi: facendo clic con il pulsante destro del mouse su **Sequenze** in Esplora oggetti e quindi scegliendo **Nuova sequenza**oppure facendo clic con il pulsante destro del mouse su una sequenza esistente e quindi scegliendo **Proprietà**. In quest'ultimo caso le opzioni in **Proprietà** non possono essere modificate. Per modificare le opzioni relative alle sequenze, usare l'istruzione [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql) oppure eliminare e ricreare l'oggetto sequenza.  
  
## <a name="options"></a>Opzioni  
 **Nome sequenza**  
 Consente di immettere il nome della sequenza.  
  
 **Schema sequenza**  
 Consente di specificare lo schema che sarà proprietario della sequenza.  
  
 **Tipo di dati**  
 Una sequenza può essere definita come qualsiasi tipo Integer. ad esempio:  
  
|Tipo di dati|Intervallo|  
|---------------|-----------|  
|`tinyint`|da 0 a 255|  
|`smallint`|Da -32.768 a 32.767|  
|`int`|Da -2.147.483.648 a 2.147.483.647|  
|`bigint`|Da -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807|  
  
-   `decimal` o `numeric` con scala 0.  
  
-   Qualsiasi tipo di dati definito dall'utente (tipo di alias) basato su uno di questi tipi.  
  
 **Precisione**  
 Consente di specificare la precisione per i tipi di dati `decimal` o `numeric` (la scala è sempre 0).  
  
 **Valore iniziale**  
 Primo valore che verrà restituito dall'oggetto sequenza. Il valore **START** deve essere minore o uguale al valore massimo e maggiore o uguale al valore minimo dell'oggetto sequenza. Il valore iniziale predefinito per un nuovo oggetto sequenza è il valore minimo per un oggetto sequenza con ordine crescente e il valore massimo per un oggetto sequenza con ordine decrescente.  
  
 **Incremento di**  
 Valore usato per incrementare (o decrementare, in caso di valore negativo) il valore dell'oggetto sequenza per ogni chiamata alla funzione **NEXT VALUE FOR** . Se l'incremento è un valore negativo, l'oggetto sequenza ha un ordine decrescente, in caso contrario avrà un ordine crescente. L'incremento non può essere 0.  
  
 **Valore minimo**  
 Specifica i limiti per l'oggetto sequenza. Il valore minimo predefinito per un nuovo oggetto sequenza è il valore minimo del tipo di dati dell'oggetto sequenza. Tale valore è zero per il tipo di dati `tinyint` e un numero negativo per tutti gli altri tipi di dati.  
  
 **Valore massimo**  
 Specifica i limiti per l'oggetto sequenza. Il valore massimo predefinito per un nuovo oggetto sequenza è il valore massimo del tipo di dati dell'oggetto sequenza.  
  
 **Riavvio sequenza ciclica al raggiungimento del limite**  
 Selezionare questa opzione per consentire il riavvio dell'oggetto sequenza dal valore minimo (o massimo per gli oggetti sequenza con ordine decrescente) quando viene superato il valore minimo o massimo.  
  
> [!NOTE]  
>  Il ciclo non ricomincia dal valore iniziale, bensì dal valore minimo/massimo.  
  
 **Opzioni cache**  
 La creazione di una cache di valori di sequenza può favorire un miglioramento delle prestazioni per applicazioni in cui vengono utilizzati oggetti sequenza, riducendo il numero di I/O su disco necessari per creare numeri di sequenza.  
  
-   Dimensioni cache predefinite: nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] vengono selezionate dimensioni specifiche, che tuttavia non devono necessariamente essere considerate coerenti. [!INCLUDE[msCoName](../../includes/msconame-md.md)] potrebbe cambiare il metodo di calcolo della dimensione della cache senza preavviso.  
  
-   Nessuna cache: in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] i numeri di sequenza non vengono memorizzati nella cache.  
  
-   Memorizzazione nella cache con dimensione: in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono memorizzati nella cache i valori di sequenza. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di tenere traccia del valore corrente e del numero di valori rimasti nella cache. La quantità di memoria richiesta per l'archiviazione della cache è pertanto sempre corrispondente a due istanze del tipo di dati dell'oggetto sequenza.  
  
 In caso di creazione con l'opzione CACHE, un arresto imprevisto quale un'interruzione dell'alimentazione, può provocare la perdita dei numeri di sequenza nella cache.  
  
 Per informazioni aggiuntive sulle opzioni di creazione di una sequenza, vedere [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql).  
  
## <a name="permissions"></a>Permissions  
 Richiede l'autorizzazione **CREATE SEQUENCE**, **ALTER**o **CONTROL** per l'oggetto SCHEMA.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sequences &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)  
  
  
