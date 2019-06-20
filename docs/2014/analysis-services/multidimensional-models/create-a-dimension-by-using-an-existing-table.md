---
title: Creare una dimensione utilizzando una tabella esistente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], dimensions
- main dimension tables
- dimensions [Analysis Services], standard
- standard dimensions [Analysis Services]
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e65c2b8d543455a168bddc1be5ae5594c2ba8c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076417"
---
# <a name="create-a-dimension-by-using-an-existing-table"></a>Creare una dimensione utilizzando una tabella esistente
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]è possibile usare Creazione guidata dimensione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per creare una dimensione da una tabella esistente. A questo scopo selezionare l'opzione **Usa una tabella esistente** nella pagina **Seleziona metodo di creazione** della procedura guidata. L'utilizzo di questa opzione fa sì che la struttura della dimensione venga creata in base alle tabelle della dimensione, alle relative colonne e a tutte le relazioni tra colonne presenti in una vista origine dati esistente. La procedura guidata campiona i dati nella tabella di origine e nelle tabelle correlate. Usa questi dati per definire le colonne attributo basate sulle colonne nelle tabelle delle dimensioni, nonché per definire le gerarchie di attributi, denominate gerarchie *definite dall'utente* . È possibile utilizzare Progettazione dimensioni al termine della Creazione guidata dimensione per aggiungere, rimuovere e configurare attributi e gerarchie nella dimensione.  
  
 Durante l’utilizzo di una tabella esistente per creare una dimensione, Creazione guidata dimensione consente di effettuare in modo semplificato i seguenti passaggi:  
  
-   Specifica delle informazioni di origine  
  
-   Selezione di tabelle correlate  
  
-   Selezione degli attributi della dimensione  
  
-   Definizione di Business Intelligence per la contabilità  
  
> [!NOTE]  
>  Per istruzioni dettagliate che corrispondono alle informazioni elencate in questo argomento, vedere [Creare una dimensione utilizzando la Creazione guidata dimensione](create-a-dimension-using-the-dimension-wizard.md).  
  
## <a name="specifying-the-source-information"></a>Specifica delle informazioni di origine  
 Specificare le informazioni di origine nella pagina **Impostazione informazioni origine** . Si inizia questo processo selezionando la vista origine dati che contiene la tabella sulla quale basare la dimensione. Specificare quindi la tabella principale della dimensione in fase di definizione. La tabella principale della dimensione è direttamente collegata alla tabella dei fatti. Specificare ad esempio una tabella Prodotto come tabella principale per una dimensione Prodotti o una tabella Dipendente per una dimensione Dipendenti. La procedura guidata seleziona automaticamente una colonna chiave basata sulla chiave primaria nella vista origine dati. Comunque, è possibile modificare in base alle proprie esigenze la colonna chiave. La colonna chiave determina i membri della dimensione. È ad esempio possibile definire ProductKey come colonna chiave per una dimensione Prodotto.  
  
 Facoltativamente, è possibile definire una colonna contenente il nome del membro. Per impostazione predefinita, il nome del membro che viene visualizzato agli utenti corrisponde al valore della colonna chiave. I valori in una colonna chiave, ad esempio ProductID o EmployeeID, sono in genere chiavi univoche generate automaticamente, non significative per l'utente. È spesso possibile fornire informazioni più significative all'utente se si modifica il nome che gli utenti vedono con un valore corrispondente in altre colonne nella dimensione. Ad esempio, è possibile definire una colonna del nome dei membri che contiene nomi di prodotto o nomi dei dipendenti. Se si modifica il nome del membro, gli utenti vedono un nome più descrittivo, ma le query utilizzano ancora i valori della colonna chiave per distinguere correttamente i membri che condividono lo stesso nome. Se si specifica una chiave composta per la colonna chiave, si deve specificare anche la colonna che fornisce i valori del membro per l'attributo chiave. Per altre informazioni su come configurare le proprietà dell'attributo, vedere [Riferimento alle proprietà degli attributo delle dimensioni](dimension-attribute-properties-reference.md).  
  
## <a name="selecting-related-tables"></a>Selezione di tabelle correlate  
  
> [!NOTE]  
>  Questo passaggio viene ignorato se nella vista origine dati non sono definite relazioni tra la tabella principale della dimensione e altre tabelle della dimensione.  
  
 In caso di compilazione di una dimensione con schema snowflake, specificare le tabelle correlate da cui verranno definiti attributi aggiuntivi nella pagina **Selezione tabelle correlate** . Ad esempio, si sta compilando una dimensione del cliente nella quale si vuole definire una tabella dei dati geografici del cliente. In questo caso, è possibile definire una tabella di dati geografici come tabella correlata.  
  
## <a name="selecting-dimension-attributes"></a>Selezione degli attributi della dimensione  
 Dopo avere selezionato tutte le tabelle dimensione, tramite la pagina **Selezione attributi dimensione** scegliere gli attributi che si desidera includere nella dimensione da tali tabelle. Tutte le colonne sottostanti di queste tabelle sono disponibili come potenziali attributi della dimensione. L'attributo chiave della dimensione deve essere selezionato e deve essere abilitato per esplorare.  
  
 Per impostazione predefinita, la procedura guidata imposta il tipo di un attributo su `Regular`. Comunque, è necessario eseguire il mapping di attributi specifici ad un tipo di attributo diverso che meglio rappresenta i dati. Ad esempio, la tabella dbo.DimAccount nel database di esempio [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW contiene una colonna AccountCodeAlternateKey che fornisce il numero del conto. Anziché impostare il tipo su `Regular` per questo attributo, si potrebbe voler eseguire il mapping di questo attributo per il `Account Number` tipo.  
  
> [!NOTE]  
>  Se il tipo di dimensione e i tipi di attributo standard non sono stati definiti al momento della creazione della dimensione, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per impostare tali valori dopo aver creato la dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per le dimensioni a una dimensione](bi-wizard-add-dimension-intelligence-to-a-dimension.md) o (per una dimensione di tipo conti) [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
 La procedura guidata imposta automaticamente il tipo di dimensione in base ai tipi di attributo specificati. I tipi di attributo specificati nella procedura guidata hanno impostato la proprietà `Type` per gli attributi. L'impostazione della proprietà `Type` per la dimensione ed i suoi attributi offre informazioni sui contenuti di una dimensione alle applicazioni server e client. In alcuni casi, l'impostazione di proprietà `Type` offre informazioni solo alle applicazioni client ed è facoltativa. In altri casi, ad esempio per le dimensioni Conto, Periodo o Valuta, le impostazioni della proprietà `Type` determinano comportamenti specifici basati sul server e possono essere necessarie per implementare determinati comportamenti del cubo.  
  
 Per altre informazioni sui tipi di dimensione e attributo, vedere [Tipi di dimensioni](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md), [Configurare tipi di attributi](attribute-properties-configure-attribute-types.md).  
  
## <a name="defining-account-intelligence"></a>Definizione di Business Intelligence per la contabilità  
  
> [!NOTE]  
>  Nella Creazione guidata dimensione, questo passaggio viene visualizzato solo se è stato definito un attributo **Tipo conto** della dimensione nella pagina **Selezione attributi di dimensione** della procedura guidata.  
  
 Si usa la pagina **Funzionalità di Business Intelligence per la contabilità** per creare una dimensione tipo Conto. Se si crea una dimensione tipo Conto, è necessario eseguire il mapping dei tipi di conto standard supportati da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ai membri dell'attributo tipo Conto nella dimensione. Il server utilizzerà tali associazioni per garantire alias e funzioni di aggregazione separati per ogni tipo di dati Conto.  
  
 Per eseguire il mapping di questi tipi di conto, la procedura guidata fornisce una tabella con le seguenti colonne:  
  
-   Nella colonna **Tipi di conto tabella di origine** vengono elencati i tipi di conto recuperati dalla tabella origine dati.  
  
-   La colonna **Tipi di conto predefiniti** elenca i tipi di conto standard corrispondenti supportati dal server. Se i dati di origine usano nomi standard, la procedura guidata consente di eseguire automaticamente il mapping del tipo di origine al tipo di server e inserisce queste informazioni nella colonna **Tipi di conto predefiniti** . Se il server non esegue il mapping dei tipi di conto o si vuole modificare il mapping, selezionare un tipo diverso dall'elenco nella colonna **Tipi di conto predefiniti** .  
  
> [!NOTE]  
>  Se i tipi di conto non sono sottoposti a mapping al momento della creazione della dimensione Conto, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per impostare tali associazioni dopo aver creato la dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="completing-the-wizard"></a>Completamento procedura guidata  
 La procedura guidata consente di eseguire l'analisi delle tabelle della dimensione per rilevare le relazioni. La procedura guidata creerà automaticamente relazioni tra attributi chiave nelle dimensioni snowflake.  
  
 La procedura guidata rileva anche automaticamente se una relazione padre-figlio esiste nella dimensione. Si ha una relazione padre-figlio quando un attributo padre fa riferimento ai membri dell'attributo chiave della dimensione. Questa relazione definisce relazioni gerarchiche e percorsi di aggregazione tra membri foglia della dimensione. Per altre informazioni sulle gerarchie padre-figlio, vedere [Attributi nelle gerarchie padre-figlio](parent-child-dimension-attributes.md).  
  
 Nella pagina **Completamento procedura guidata** si completa la procedura guidata digitando un nome per la dimensione nuova e rivedendo la struttura della dimensione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una dimensione generando una tabella non temporale nell'origine dati](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)   
 [Riferimento alle proprietà degli attributo delle dimensioni](dimension-attribute-properties-reference.md)   
 [Create a Time Dimension by Generating a Time Table](create-a-time-dimension-by-generating-a-time-table.md)   
 [Creare una dimensione generando una tabella non temporale nell'origine dati](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
