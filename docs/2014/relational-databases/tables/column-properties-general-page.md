---
title: Proprietà colonna (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.columnproperties.general.f1
ms.assetid: a745890b-994e-4c23-8028-5c83751e60c4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 741c8633a9b7eed9fcd253918c34a27119e51ee4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62854903"
---
# <a name="column-properties-general-page"></a>Proprietà colonna (pagina Generale)
  Utilizzare questa pagina per visualizzare le proprietà per la colonna selezionata.  
  
 Le informazioni visualizzate in questa pagina sono di sola lettura. Per modificare la colonna chiudere la finestra di dialogo **Proprietà colonna** , espandere la tabella e le colonne in Esplora oggetti, fare clic con il pulsante destro del mouse sulla colonna e quindi scegliere **Progetta**.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Nome della colonna.  
  
 **Tipo di dati**  
 Tipo di dati che è possibile inserire nella colonna. Se il tipo di dati è un tipo di dati definito dall'utente, verrà visualizzato il tipo di dati definito dall'utente. Se il tipo di dati non è un tipo di dati definito dall'utente, viene visualizzato il tipo di dati di sistema. Per altre informazioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
 **Tipo di sistema**  
 Tipo di dati che è possibile inserire nella colonna. Se il tipo di dati è un tipo di dati di sistema, viene visualizzato il tipo di dati di sistema. Se il tipo di dati è un tipo di dati definito dall'utente, viene visualizzato il tipo di dati di sistema che costituisce il tipo di dati definito dall'utente.  
  
 **Chiave primaria**  
 Indica se la colonna è una chiave primaria. I valori possibili sono **True**e **False**.  
  
 **Consenti valori NULL**  
 Indica se la colonna accetta valori NULL. I valori possibili sono **True** e **False**.  
  
 **Calcolato**  
 Indica se il valore di colonna è il risultato di un'espressione calcolata.  
  
 **Testo calcolato**  
 Indica l'istruzione utilizzata per il calcolo dell'espressione del testo della colonna. Per altre informazioni, vedere [Specificare le colonne calcolate in una tabella](specify-computed-columns-in-a-table.md).  
  
 **Identità**  
 Indica se la colonna è la colonna Identity per la tabella. I valori possibili sono **True** e **False**.  
  
 **Valore di inizializzazione Identity**  
 Indica il valore di riga iniziale per una colonna Identity.  
  
 **Incremento identità**  
 La proprietà **Incremento Identity** specifica il valore aggiunto da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al valore Identity di riga massimo esistente nel momento in cui viene generato un valore Identity per la riga di cui viene eseguito l'inserimento.  
  
 **Binding predefinito**  
 Valore predefinito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associato alla colonna. Se non è associato alcun valore predefinito, questa opzione è vuota.  
  
 **Schema predefinito**  
 Identifica lo schema di database a cui appartiene il valore predefinito associato alla colonna. Se non è associato alcun valore predefinito, questa opzione è vuota.  
  
 **Regola**  
 Identifica il vincolo di integrità dei dati associato alla colonna. Se non è associata alcuna regola questa opzione è vuota.  
  
 **Schema regola**  
 Visualizza lo schema di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui appartiene la regola associata alla colonna. Se non è associata alcuna regola questa opzione è vuota.  
  
 **Length**  
 Indica il numero massimo di caratteri o byte accettati dalla colonna.  
  
 **Regole di confronto**  
 Visualizza le regole di confronto correnti per la colonna. Se non è indicato alcun valore, la proprietà relativa alle regole di confronto viene ereditata dall'oggetto.  
  
 **Precisione numerica**  
 Indica il numero massimo di cifre per un tipo di dati numerico a precisione fissa.  
  
 **Scala numerica**  
 Indica il numero di cifre a destra del punto decimale per un tipo di dati numerico a precisione fissa.  
  
 **Spazio dei nomi XML Schema**  
 Definisce il tipo di colonna XML tramite la convalida del linguaggio XML Schema Definition (XSD).  
  
 **Schema dello spazio dei nomi XML Schema**  
 Schema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui appartiene lo spazio dei nomi dell'XML Schema.  
  
> [!NOTE]  
>  Il termine schema può avere significati diversi. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa uno schema per organizzare gli oggetti di database. In questo contesto è sinonimo di proprietà. XML utilizza lo schema per definire l'organizzazione delle informazioni XML in una serie di spazi dei nomi. Si tratta di una modalità di raggruppamento del codice XML correlato.  
  
 **Sparse**  
 Indica se la colonna è una colonna di tipo sparse. I valori possibili sono **True** e **False**. Per altre informazioni, vedere [Usare le colonne di tipo sparse](use-sparse-columns.md).  
  
 **Set di colonne**  
 Indica se la colonna è un set di colonne. I valori possibili sono **True** e **False**. Per altre informazioni, vedere [Usare set di colonne](use-column-sets.md).  
  
 **Stato riempimento ANSI**  
 Indica se il riempimento ANSI è attivato o disattivato. Per altre informazioni, vedere [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Testo completo**  
 Indica se la colonna viene utilizzata nelle query full-text.  
  
 **Semantica statistica**  
 Indica se la ricerca semantica statistica è abilitata per la colonna. Per altre informazioni, vedere [Ricerca semantica &#40;SQL Server&#41;](../search/semantic-search-sql-server.md).  
  
 **Non per la replica**  
 Indica se la colonna è disponibile per la replica. I valori possibili sono **True** e **False**.  
  
  
