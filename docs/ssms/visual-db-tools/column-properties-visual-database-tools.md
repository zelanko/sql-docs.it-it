---
description: Proprietà colonne (Visual Database Tools)
title: Proprietà delle colonne
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.Column.ColumnIdentitySpec
- vdt.designers.properties.Column
- vdt.tablecolumn
- vdt.designers.properties.Column.ColumnComputedColumnSpec
- vdt.designers.properties.Column.ColumnFulltextSpec
ms.assetid: e549a2a8-4154-4ec8-b146-614564169b39
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2228819de295edf29d5b2b1ca6bfcc43626a42a0
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038937"
---
# <a name="column-properties-visual-database-tools"></a>Proprietà colonne (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Per le colonne sono disponibili due set di proprietà: il set completo, visualizzabile nella scheda **Proprietà colonna** in Progettazione tabelle (disponibile solo per i database di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e un subset, visualizzabile nella finestra Proprietà in Esplora server.  
  
> [!NOTE]  
> Le proprietà illustrate in questo argomento sono ordinate per categoria anziché alfabeticamente.  
  
> [!NOTE]  
> È possibile che le finestre di dialogo e i comandi di menu visualizzati varino da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** .  
  
## <a name="properties-window"></a>Finestra Proprietà  
Queste proprietà vengono visualizzate nella finestra Proprietà quando si seleziona una colonna in Esplora server.  
  
> [!NOTE]  
> Queste proprietà, a cui si accede da Esplora server, sono di sola lettura. Per modificare le proprietà delle colonne dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare la colonna in Progettazione tabelle. Le proprietà sono descritte di seguito in questo argomento.  
  
**Categoria Identità**  
Viene espansa per visualizzare le proprietà **Nome** e **Database** .  
  
**Nome**  
Consente di visualizzare il nome della colonna.  
  
**Database**  
Consente di visualizzare il nome dell'origine dei dati della colonna selezionata (solo per OLE DB).  
  
**Categoria Varie**  
Viene espansa per visualizzare le proprietà rimanenti.  
  
**Tipo di dati**  
Mostra il tipo di dati della colonna selezionata. Per altre informazioni, vedere [Tipi di dati (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md).  
  
**Incremento identità**  
Mostra l'incremento che verrà aggiunto a **Valore di inizializzazione Identity** per ogni riga successiva della colonna Identity e (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
**Valore di inizializzazione Identity**  
Consente di visualizzare il valore di inizializzazione assegnato alla prima riga della tabella per la colonna di identità (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
**Identità**  
Indica se la colonna selezionata è la colonna di identità per la tabella. (si applica solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
**Lunghezza**  
Indica il numero di caratteri consentiti per i tipi di dati basati su caratteri.  
  
**Ammette i valori Null**  
Indica se la colonna accetta valori Null.  
  
**Precisione**  
Indica il numero massimo di cifre ammesse per i tipi di dati numerici. Questa proprietà corrisponde a **0** per i tipi di dati non numerici.  
  
**Ridimensionamento**  
Indica il numero massimo di cifre ammesse dopo la virgola decimale nei tipi di dati numerici. Questo valore deve essere inferiore o uguale al valore di precisione. Questa proprietà corrisponde a **0** per i tipi di dati non numerici.  
  
## <a name="column-properties-tab"></a>Scheda Proprietà colonne  
Per accedere a queste proprietà, in Esplora server fare clic con il pulsante destro del mouse sulla tabella a cui appartiene la colonna, scegliere **Apri definizione tabella**e selezionare la riga nella griglia della tabella in Progettazione tabelle.  
  
> [!NOTE]  
> Queste proprietà si applicano solo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Categoria Generale**  
Viene espansa per visualizzare le proprietà **Nome**, **Consenti valori Null**, **Tipo di dati**, **Valore predefinito dell'associazione**, **Lunghezza**, **Precisione**e **Scala**.  
  
**Nome**  
Consente di visualizzare il nome della colonna. Per modificare il nome, digitarlo nella casella di testo.  
  
> [!CAUTION]  
> Se query, viste, funzioni definite dall'utente, stored procedure o programmi esistenti fanno riferimento alla tabella, la modifica del nome renderà non validi tali oggetti.  
  
**Consenti valori NULL**  
Indica se il tipo di dati della colonna accetta valori Null.  
  
**Tipo di dati**  
Consente di visualizzare il tipo di dati della colonna selezionata. Per modificare questa proprietà, fare clic sul valore, espandere l'elenco a discesa e selezionare un nuovo valore. Per altre informazioni, vedere [Tipi di dati (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md).  
  
**Valore predefinito o associazione**  
Mostra il valore predefinito utilizzato per la colonna quando non ne viene specificato alcuno. Nell'elenco a discesa sono contenuti tutti i valori predefiniti globali impostati nell'origine dei dati. Per associare la colonna a un valore predefinito globale, selezionarlo dall'elenco a discesa. In alternativa, per creare un vincolo predefinito per la colonna, digitare direttamente il valore predefinito come testo.  
  
**Lunghezza**  
Indica il numero di caratteri consentiti per i tipi di dati basati su caratteri. Questa proprietà è disponibile solo per tipi di dati basati su caratteri.  
  
**Precisione**  
Indica il numero massimo di cifre ammesse per i tipi di dati numerici. Questa proprietà corrisponde a **0** per i tipi di dati non numerici. Questa proprietà è disponibile solo per tipi di dati numerici.  
  
**Ridimensionamento**  
Indica il numero massimo di cifre ammesse dopo la virgola decimale nei tipi di dati numerici. Questo valore deve essere inferiore o uguale al valore di precisione. Questa proprietà corrisponde a **0** per i tipi di dati non numerici. Questa proprietà è disponibile solo per tipi di dati numerici.  
  
**Categoria Progettazione tabelle**  
Viene espansa per visualizzare le proprietà rimanenti.  
  
**Regole di confronto**  
Indica l'impostazione delle regole di confronto per la colonna selezionata. Per modificare questa impostazione, scegliere **Regole di confronto** e fare clic sui puntini di sospensione **(...)** a destra del valore.  
  
**Categoria Specifica colonna calcolata**  
Si espande per visualizzare le proprietà **Formula** e **Persistente**. Se la colonna è calcolata, verrà visualizzata anche la formula. Per modificare la formula, espandere questa categoria e apportare la modifica nella proprietà **Formula** .  
  
**Formula**  
Consente di visualizzare la formula se la colonna selezionata è una colonna calcolata. Utilizzare questo campo per immettere o modificare una formula.  
  
**Persistente**  
Consente di salvare la colonna calcolata con l'origine dei dati. Una colonna calcolata persistente può essere indicizzata.  
  
**Tipo di dati abbreviato**  
Consente di visualizzare informazioni sul tipo di dati del campo, nello stesso formato dell'istruzione SQL CREATE TABLE. Un campo contenente ad esempio una stringa di lunghezza variabile con un massimo di 20 caratteri viene rappresentato come "varchar(20)". Per modificare questa proprietà, digitare direttamente il valore desiderato.  
  
**Descrizione**  
Consente di visualizzare la descrizione della colonna. Per visualizzare la descrizione completa o modificarla, fare clic su Descrizione e sui puntini di sospensione **(...)** a destra della proprietà.  
  
**Categoria Specifica full-text**  
Viene espansa per visualizzare le proprietà specifiche per le colonne full-text.  
  
**Con indice full-text**  
Indica se la colonna è indicizzata con un indice full-text. Questa proprietà può essere impostata su **Sì** solo se il tipo di dati della colonna consente ricerche full-text e se per la tabella a cui la colonna appartiene è specificato un indice full-text. Per modificare questo valore, fare clic su di esso, espandere l'elenco a discesa e selezionare un nuovo valore.  
  
**Colonna di tipo full-text**  
Indica la colonna utilizzata per definire il tipo di documento di una colonna di tipo image. Il tipo di dati image può essere utilizzato per archiviare diversi tipi di documenti, tra cui doc e xml.  
  
**Lingua**  
Indica il linguaggio utilizzato per indicizzare la colonna.  
  
**Semantica statistica**  
Selezionare se abilitare l'indicizzazione semantica statistica per la colonna selezionata. Per altre informazioni, vedere [Ricerca semantica](../../relational-databases/search/semantic-search-sql-server.md).  
  
Se si seleziona una lingua in **Lingua** prima di selezionare **Semantica statistica**e alla lingua selezionata non è associato alcun modello di lingua semantico, l'opzione **Semantica statistica** viene impostata su **No** e non può essere modificata. Se si seleziona **Sì** per l'opzione **Semantica statistica** prima di selezionare una lingua in **Lingua**, le lingue disponibili nella colonna **Lingua** saranno limitate a quelle per cui è disponibile un modello di lingua semantico.  
  
**Con Sottoscrittore non SQL Server**  
Indica se la colonna è associata a un Sottoscrittore SQL Server non Microsoft.  
  
**Categoria Specifica identità**  
Si espande per visualizzare le proprietà **Identity**, **Incremento Identity**e **Valore di inizializzazione identity**.  
  
**Identità**  
Indica se la colonna selezionata è la colonna di identità per la tabella. Per modificare la proprietà, aprire la tabella in Progettazione tabelle e apportare le modifiche nella finestra **Proprietà** . Questa impostazione è valida solo per le colonne con tipo di dati numerico, ad esempio *int*.  
  
**Incremento identità**  
Visualizza l'incremento che verrà aggiunto al valore di **Valore di inizializzazione Identity** per ogni riga successiva. Se si lascia vuota questa cella, verrà assegnato un valore predefinito pari a 1. Per modificare questa proprietà, digitare direttamente il nuovo valore.  
  
**Valore di inizializzazione Identity**  
Indica il valore assegnato alla prima riga della tabella. Se si lascia vuota questa cella, verrà assegnato un valore predefinito pari a 1. Per modificare questa proprietà, digitare direttamente il nuovo valore.  
  
**Deterministico**  
Indica se il tipo di dati della colonna selezionata può essere determinato con certezza.  
  
**Con pubblicazione di tipo DTS**  
Indica se la pubblicazione della colonna è di tipo DTS.  
  
**Is Indexable**  
Indica se la colonna selezionata può essere indicizzata. Le colonne calcolate non deterministiche, ad esempio, non sono indicizzabili.  
  
**Con pubblicazione di tipo merge**  
Indica se la pubblicazione della colonna è di tipo merge.  
  
**Non per la replica**  
Indica se durante la replica vengono mantenuti i valori di identità originari. Per modificare questa proprietà, fare clic sul valore, espandere l'elenco a discesa e selezionare un nuovo valore.  
  
**Replicato**  
Indica se questa colonna è replicata in un'altra posizione.  
  
**RowGuid**  
Indica se la colonna viene utilizzata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come ROWGUID. Questo valore può essere impostato su **Sì** solo per una colonna con tipo di dati **uniqueidentifier**. Per modificare questa proprietà, fare clic sul valore, espandere l'elenco a discesa e selezionare un nuovo valore.  
  
**Dimensione**  
Indica la dimensione in byte consentita dal tipo di dati della colonna. Ad esempio, un tipo di dati **nchar** può avere una lunghezza di 10 (il numero di caratteri), ma avrebbe una dimensione di 20 per quanto riguarda i set di caratteri Unicode.  
  
> [!NOTE]  
> La lunghezza di un tipo di dati **varchar(max)** varia per ogni riga. sp_help restituisce (-1) come lunghezza della colonna **varchar(max)** . [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] visualizza -1 come dimensione della colonna.  
