---
title: Requisiti per le aggregazioni CLR definite dall'utente Documenti Microsoft
description: L'integrazione CLR di SQL Server consente di creare funzioni di aggregazione personalizzate nel codice gestito. Devono implementare il contratto di aggregazione richiesto.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd27cf3751400d3902ddd4199daee8aeef78b80
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487951"
---
# <a name="clr-user-defined-aggregates---requirements"></a>Aggregazioni CLR definite dall'utente - Requisiti
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un tipo in un assembly CLR (Common Language Runtime) può essere registrato come funzione di aggregazione definita dall'utente, purché implementi il contratto di aggregazione necessario. Questo contratto è costituito dall'attributo **SqlUserDefinedAggregate** e dai metodi del contratto di aggregazione. Il contratto di aggregazione include il meccanismo per salvare lo stato intermedio dell'aggregazione e il meccanismo per accumulare nuovi valori, costituito da quattro metodi: **Init**, **Accumulate**, **Merge**e **Terminate**. Una volta soddisfatti questi requisiti, sarà possibile sfruttare appieno le [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aggregazioni definite dall'utente in . Nelle sezioni seguenti di questo argomento sono disponibili altre informazioni dettagliate su come creare e utilizzare aggregazioni definite dall'utente. Per un esempio, vedere Richiamo di funzioni di [aggregazione CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Per ulteriori informazioni, vedere [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Metodi di aggregazione  
 La classe registrata come aggregazione definita dall'utente deve supportare i metodi di istanza seguenti. Tali metodi vengono utilizzati da Query Processor per calcolare l'aggregazione:  
  
|Metodo|Sintassi|Descrizione|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|Query Processor utilizza questo metodo per inizializzare il calcolo dell'aggregazione. Questo metodo viene richiamato una volta per ogni gruppo aggregato da Query Processor. Query Processor può scegliere di riutilizzare la stessa istanza della classe di aggregazione per il calcolo delle aggregazioni di più gruppi. Il **init** metodo deve eseguire qualsiasi pulizia in base alle esigenze degli utilizzi precedenti di questa istanza e consentire di riavviare un nuovo calcolo di aggregazione.|  
|**Accumulare**|`public void Accumulate ( input-type value[, input-type value, ...]);`|Uno o più parametri che rappresentano i parametri della funzione. *input_type* deve essere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati gestiti equivalente al tipo di dati nativo specificato da *input_sqltype* nell'istruzione **CREATE AGGREGATE.** Per ulteriori informazioni, vedere [Mapping dei dati dei parametri CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Per i tipi definiti dall'utente (UDT, User-Defined Type), il tipo di input coincide con il tipo definito dall'utente. Query Processor utilizza questo metodo per accumulare i valori di aggregazione. Il metodo viene richiamato una volta per ogni valore nel gruppo aggregato. Query Processor chiama sempre questo solo dopo aver chiamato il **Init** metodo sull'istanza specificata della classe di aggregazione. L'implementazione di questo metodo deve aggiornare lo stato dell'istanza per riflettere l'accumulazione del valore dell'argomento passato.|  
|**Unione**|`public void Merge( udagg_class value);`|Questo metodo può essere utilizzato per unire un'altra istanza di questa classe di aggregazione all'istanza corrente. Query Processor utilizza questo metodo per unire più calcoli parziali di un'aggregazione.|  
|**Terminare**|`public return_type Terminate();`|Questo metodo completa il calcolo di aggregazione e restituisce il risultato dell'aggregazione. Il *return_type* deve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] essere un tipo di dati gestiti equivalente all'equivalente gestito di *return_sqltype* specificato nell'istruzione **CREATE AGGREGATE.** Il *return_type* può anche essere un tipo definito dall'utente.|  
  
### <a name="table-valued-parameters"></a>Parametri con valori di tabella  
 I parametri con valori di tabella, ovvero tipi di tabella definiti dall'utente passati in una procedura o in una funzione, consentono di passare in modo efficiente più righe di dati al server. Pur essendo caratterizzati da funzionalità simili alle matrici di parametri, i parametri con valori di tabella offrono più flessibilità e una maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)] Consentono inoltre di ottenere prestazioni potenzialmente migliori. I parametri con valori di tabella consentono inoltre di ridurre il numero di round trip al server. Anziché inviare più richieste al server, ad esempio con un elenco di parametri scalari, è possibile inviare i dati al server sotto forma di parametro con valori di tabella. Un tipo di tabella definito dall'utente non può essere passato come parametro con valori di tabella a una stored procedure gestita o a una funzione in esecuzione nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], né può essere restituito dalle stesse. I parametri con valori di tabella, inoltre, non possono essere utilizzati nell'ambito di una connessione di contesto. È tuttavia possibile utilizzare un parametro con valori di tabella con SqlClient in stored procedure o funzioni gestite eseguite nel processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se utilizzato in una connessione diversa da una connessione di contesto. La connessione può essere stabilita con lo stesso server che esegue la funzione o la procedura gestita. Per ulteriori informazioni sui programmi TV, vedere Usare parametri con valori di [tabella &#40;&#41;del motore di database ](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Aggiornata la descrizione del metodo **Accumulate;** ora accetta più di un parametro.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Chiamata di funzioni di aggregazione CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
