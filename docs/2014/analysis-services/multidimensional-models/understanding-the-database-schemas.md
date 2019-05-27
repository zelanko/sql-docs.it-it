---
title: Informazioni sugli schemi di Database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, database schema
- database schema [Analysis Services]
- relational schema [Analysis Services], database schema
- subject area schema options [Analysis Services]
- staging area schema options [Analysis Services]
- denormalized schemas
ms.assetid: 51e411f9-ee3f-4b92-9833-c2bce8c6b752
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b3439fff5e3bba68f01c24a0979434e21a01ded6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072713"
---
# <a name="understanding-the-database-schemas"></a>Informazioni sugli schemi di database
  La Generazione guidata schema consente di generare uno schema relazionale denormalizzato per il database dell'area di interesse in base alle dimensioni e ai gruppi di misure in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La procedura guidata genera una tabella relazionale per ogni dimensione, denominata tabella della dimensione, in cui vengono archiviati i dati della dimensione e una tabella relazionale per ogni gruppo di misure, denominata tabella dei fatti, in cui vengono archiviati i fatti. Durante la generazione di queste tabelle relazionali, la procedura guidata ignora dimensioni collegate, gruppi di misure collegati e dimensioni temporali del server.  
  
## <a name="validation"></a>Convalida  
 Prima di iniziare a generare lo schema relazionale sottostante, la Generazione guidata schema convalida i cubi e le dimensioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se vengono rilevati alcuni errori, la procedura guidata viene arrestata e gli errori vengono visualizzati nella finestra Elenco attività di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Di seguito sono riportati alcuni esempi di errori che impediscono la generazione:  
  
-   Dimensioni con più attributi chiave.  
  
-   Attributi padre con tipi di dati diversi rispetto agli attributi chiave.  
  
-   Gruppi di misure privi di misure.  
  
-   Dimensioni o misure degenerate configurate in modo non corretto.  
  
-   Chiavi surrogate configurate in modo non corretto, ad esempio più attributi con il tipo di attributo `ScdOriginalID` oppure un attributo con `ScdOriginalID` non associato a una colonna con il tipo di dati integer.  
  
## <a name="dimension-tables"></a>Tabelle delle dimensioni  
 Per ogni dimensione la Generazione guidata schema genera una tabella della dimensione da includere nel database dell'area di interesse. La struttura della tabella della dimensione dipende dalle scelte effettuate durante la progettazione della dimensione su cui si basa.  
  
 Colonne  
 La procedura guidata genera una colonna per le associazioni di ogni attributo nella dimensione su cui si basa la tabella della dimensione, ad esempio le associazioni per le proprietà `KeyColumns`, `NameColumn`, `ValueColumn`, `CustomRollupColumn`, `CustomRollupPropertiesColumn` e `UnaryOperatorColumn` di ogni attributo.  
  
 Relazioni  
 La procedura guidata genera una relazione tra la colonna di ogni attributo padre e la chiave primaria della tabella della dimensione.  
  
 Se applicabile, viene inoltre generata una relazione con la chiave primaria di ogni tabella della dimensione aggiuntiva definita come dimensione di riferimento nel cubo.  
  
 Vincoli  
 Per impostazione predefinita, la procedura guidata genera per ogni tabella della dimensione un vincolo di chiave primaria basato sull'attributo chiave della dimensione. Se viene generato il vincolo di chiave primaria, per impostazione predefinita viene generata una colonna del nome separata. La chiave primaria logica viene creata nella vista origine dati anche se si decide di non creare la chiave primaria nel database.  
  
> [!NOTE]  
>  Se nella dimensione su cui si basa la tabella della dimensione vengono specificati più attributi chiave, si verifica un errore.  
  
 Traduzioni  
 La procedura guidata genera una tabella separata per l'archiviazione dei valori tradotti per ogni attributo che richiede una colonna per la traduzione. La procedura guidata crea inoltre una colonna separata per ogni lingua in cui i valori devono essere tradotti.  
  
## <a name="fact-tables"></a>Tabelle dei fatti  
 Per ogni gruppo di misure in un cubo la Generazione guidata schema genera una tabella dei fatti da includere nel database dell'area di interesse. La struttura della tabella dei fatti dipende dalle scelte effettuate durante la progettazione del gruppo di misure su cui si basa e dalle relazioni stabilite tra il gruppo di misure e qualsiasi dimensione inclusa.  
  
 Colonne  
 La procedura guidata genera una colonna per ogni misura, escluse le misure che utilizzano la funzione di aggregazione `Count`. Queste misure non richiedono una colonna corrispondente nella tabella dei fatti.  
  
 Se applicabile, la procedura guidata genera inoltre una colonna per ogni colonna dell'attributo di granularità di ogni relazione di tipo Regolare tra la dimensione e il gruppo di misure e una o più colonne per le associazioni di ogni attributo di una dimensione collegata da una relazione di tipo Fatti con il gruppo di misure sui cui si basa la tabella.  
  
 Relazioni  
 La procedura guidata genera una relazione per ogni relazione di tipo Regolare tra la tabella dei fatti e l'attributo di granularità della tabella della dimensione. Se la granularità si basa sull'attributo chiave della tabella della dimensione, la relazione viene creata nel database e nella vista origine dati. Se la granularità si basa su un altro attributo, la relazione viene creata solo nella vista origine dati.  
  
 Se si è scelto di generare gli indici nella procedura guidata, per ogni colonna delle relazioni verrà generato un indice non cluster.  
  
 Vincoli  
 Le chiave primarie non vengono generate nelle tabelle dei fatti.  
  
 Se si è scelto di applicare l'integrità referenziale, dove applicabile verranno generati vincoli di integrità referenziale tra le tabelle delle dimensioni e le tabelle dei fatti.  
  
 Traduzioni  
 La procedura guidata genera una tabella separata per l'archiviazione dei valori tradotti per ogni proprietà nel gruppo di misure che richiede una colonna per la traduzione. La procedura guidata crea inoltre una colonna separata per ogni lingua in cui i valori devono essere tradotti.  
  
## <a name="data-type-conversion-and-default-lengths"></a>Conversione del tipo di dati e lunghezze predefinite  
 Generazione guidata schema Ignora sempre i tipi di dati eccetto le colonne che usano il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `wchar` tipo di dati. La dimensione dei dati `wchar` viene convertita direttamente nel tipo di dati `nvarchar`. Tuttavia, se la lunghezza specificata di una colonna con il tipo di dati `wchar` è maggiore di 4000 byte, la Generazione guidata schema genererà un errore.  
  
 Se per un elemento di dati, ad esempio l'associazione di un attributo, non è stata specificata la lunghezza, per la colonna verrà utilizzata la lunghezza predefinita specificata nella tabella seguente.  
  
|Elemento di dati|Lunghezza predefinita (byte)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulla generazione incrementale](understanding-incremental-generation.md)   
 [Gestire modifiche a viste origine dati e origini dati](manage-changes-to-data-source-views-and-data-sources.md)  
  
  
