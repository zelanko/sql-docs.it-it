---
title: Risolvere i problemi nell'indicizzazione full-text | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d8dd1cd471328859dd8bfa595fc341bda5f51f04
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68095299"
---
# <a name="troubleshoot-full-text-indexing"></a>Risoluzione dei problemi nell'indicizzazione full-text
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
     
##  <a name="troubleshoot-full-text-indexing-failures"></a><a name="failure"></a> Risoluzione degli errori nell'indicizzazione full-text  
 Durante il popolamento o la gestione di un indice full-text, l'indicizzatore full-text potrebbe non eseguire correttamente l'indicizzazione di una o più righe per i motivi descritti di seguito. Questi errori a livello di riga non impediscono il completamento del popolamento. L'indicizzatore ignora queste righe, pertanto non sarà possibile recuperare il contenuto di tali righe tramite query.  
  
 È possibile che si verifichino errori di indicizzazione nelle situazioni seguenti.  
  
-   Quando l'indicizzatore non è in grado di trovare o caricare un componente filtro o word breaker. Questo errore può verificarsi se la riga della tabella include contenuto o un formato di documento in una lingua non registrata con l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure se il componente filtro o word breaker registrato non è stato firmato o non ha superato il controllo della firma durante il caricamento.  
  
-   Quando un componente, ad esempio un word breaker o un filtro, restituisce un errore all'indicizzatore. Questo errore può verificarsi se il documento di cui si sta eseguendo l'indicizzazione è danneggiato e il filtro non è in grado di estrarre il testo dal documento oppure quando un componente non è in grado di gestire il contenuto di una singola riga oltre una determinata dimensione, a causa di limiti di memoria nell'host del daemon dei filtri full-text (fdhost.exe).  
  
 Per ogni errore a livello di riga, nel log di tipo ricerca per indicizzazione vengono inserite informazioni sul motivo dell'errore. Il numero di errori è riepilogato al termine di un popolamento completo o incrementale.  
  
 Esistono altri errori che possono influire sul processo di indicizzazione e impedire il completamento del popolamento.  
  
-   L'indice full-text supera il limite del numero di righe che è possibile inserire in un catalogo full-text.  
  
-   Un indice cluster o un indice di chiave full-text della tabella indicizzata viene danneggiato, eliminato o ricompilato.  
  
-   Un errore hardware o del disco provoca il danneggiamento del catalogo full-text.  
  
-   Un gruppo di file contenente la tabella indicizzata full-text passa alla modalità offline o viene impostato in sola lettura.  
  
 Esaminare il log di ricerca per indicizzazione al termine di tutte le operazioni di popolamento dell'indice full-text significative o quando il popolamento non risulta completato.  
  
### <a name="unsigned-components"></a>Componenti non firmati  
 Per impostazione predefinita, l'indicizzatore full-text richiede la firma dei filtri e dei word breaker caricati. Se tali componenti non sono firmati, ad esempio in alcuni casi di installazione di componenti personalizzati, è necessario configurare l'indicizzatore full-text in modo che ignori il controllo della firma.  
  
> [!IMPORTANT]  
>  Questa impostazione rende tuttavia l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] meno sicura. È consigliabile firmare tutti i componenti implementati o assicurarsi che tutti i componenti acquistati siano firmati. Per informazioni sulle firme dei componenti, vedere [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
  
##  <a name="full-text-index-in-inconsistent-state-after-transaction-log-restored"></a><a name="state"></a> Stato incoerente di un indice full-text dopo il ripristino del log delle transazioni  
 Durante il ripristino del log delle transazioni di un database, è possibile che venga visualizzato un avviso che indica che lo stato dell'indice full-text non è coerente. Questo accade perché l'indice full-text di una tabella è stato modificato dopo il backup del database. Per riportare l'indice full-text a uno stato coerente, è necessario eseguire un popolamento completo (ricerca per indicizzazione) della tabella. Per altre informazioni sugli indici full-text, vedere [Popolamento degli indici full-text](../../relational-databases/search/populate-full-text-indexes.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [Popolamento degli indici full-text](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
