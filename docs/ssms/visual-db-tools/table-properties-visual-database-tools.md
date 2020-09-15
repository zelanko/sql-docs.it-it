---
description: Proprietà delle tabelle (Visual Database Tools)
title: Table Properties
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2c82638c23213db41aece277812522eb40a52e66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88312817"
---
# <a name="table-properties-visual-database-tools"></a>Proprietà delle tabelle (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Queste proprietà vengono visualizzate nella finestra Proprietà quando si fa clic con il pulsante destro del mouse in Progettazione tabelle e si sceglie Proprietà. Se non specificato diversamente, è possibile modificare tali proprietà nella finestra Proprietà, quando la tabella desiderata è selezionata.  
  
> [!NOTE]  
> Se la tabella viene pubblicata per la replica, è necessario apportare modifiche allo schema usando l'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) di Transact-SQL oppure SMO (SQL Server Management Objects). Quando si apportano modifiche allo schema utilizzando Progettazione tabelle o Progettazione diagrammi di database, viene effettuato il tentativo di rimuovere e rigenerare la tabella. La modifica allo schema non riuscirà, poiché non è consentita la rimozione di oggetti pubblicati.  
  
## <a name="show-table-properties-in-table-designer"></a>Per visualizzare le proprietà delle tabelle in Progettazione tabelle  
  
> [!NOTE]  
> Le proprietà illustrate in questo argomento sono ordinate per categoria anziché alfabeticamente.  
  
**Categoria Identità**  
Viene espansa per visualizzare le proprietà **Nome**, **Descrizione**e **Schema**.  
  
**Nome**  
Visualizza il nome della tabella. Per modificare il nome, digitarlo nella casella di testo.  
  
> [!CAUTION]  
> Se query, viste, funzioni definite dall'utente, stored procedure o programmi esistenti fanno riferimento alla tabella, la modifica del nome renderà non validi tali oggetti.  
  
**Nome database**  
Visualizza il nome dell'origine dati della tabella selezionata.  
  
**Descrizione**  
Visualizza una descrizione della tabella selezionata. Per visualizzare la descrizione completa o modificarla, fare clic su di essa e quindi sui puntini di sospensione **(...)** a destra della proprietà.  
  
**Schema**  
Visualizza il nome dello schema a cui appartiene la tabella (si applica solo a Microsoft SQL Server).  
  
**Nome server**  
Visualizza il nome del server dell'origine dati.  
  
**Categoria Progettazione tabelle**  
Viene espansa per visualizzare le proprietà **Colonna Identity**, **Is Indexable**e **Is Replicated**.  
  
**Colonna Identity**  
Visualizza la colonna utilizzata come colonna Identity della tabella. Per cambiare la colonna di identità, selezionare nell'elenco a discesa la colonna desiderata. Nell'elenco saranno visualizzate solo le colonne con tipo di dati numerico.  
  
**Is Indexable**  
Indica se la tabella può essere indicizzata. Se la tabella non è indicizzabile, è possibile che non appartenga all'utente o che contenga colonne con tipi di dati text, ntext o image.  
  
**Replicato**  
Indica se la tabella è replicata in un'altra posizione  
  
**Categoria Specifica spazio dei dati regolare**  
Viene espansa per visualizzare le proprietà **(Tipo spazio dei dati)**, **Nome gruppo di file o schema di partizione**ed **Elenco colonne di partizione**.  
  
**(Tipo spazio dei dati)**  
Indica se la tabella viene archiviata utilizzando un filegroup o uno schema di partizione.  
  
**Nome gruppo di file o schema di partizione**  
Visualizza il nome del filegroup o dello schema di partizione.  
  
**Elenco colonne di partizione**  
Consente di accedere alla finestra di dialogo **Elenco colonne di partizione** .  
  
**Colonna GUID riga**  
Visualizza la colonna utilizzata da Microsoft SQL Server come colonna ROWGUID della tabella. Per cambiare la colonna ROWGUID, selezionare nell'elenco a discesa la colonna desiderata (si applica solo a SQL Server 7.0 o versione successiva).  
  
**Gruppo di file Text/Image**  
Consente di selezionare nell'elenco a discesa il filegroup per le colonne con tipi di dati text o image. Se la tabella viene archiviata utilizzando uno schema di partizione, lasciare vuoto il campo.  
  
## <a name="see-also"></a>Vedere anche  
[Progettare tabelle](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
