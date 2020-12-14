---
title: Mapping di DataAdapter, DataTable e DataColumn
description: Descrive come configurare DataTableMappings e ColumnMappings per DataAdapter.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e8b2f84fbbf888fc67cdb8f945d7f0c887c14eaa
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772258"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>Mapping di DataAdapter, DataTable e DataColumn

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Una classe <xref:Microsoft.Data.SqlClient.SqlDataAdapter> contiene una raccolta di zero o più oggetti <xref:System.Data.Common.DataTableMapping> nella proprietà <xref:System.Data.Common.DataAdapter.TableMappings%2A>. Un oggetto **DataTableMapping** fornisce un mapping principale tra i dati restituiti da una query eseguita su un'origine dati e una classe <xref:System.Data.DataTable>. Al posto del nome della classe **DataTable** è possibile passare il nome di **DataTableMapping** al metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A> di **DataAdapter**. L'esempio seguente crea un oggetto **DataTableMapping** denominato **AuthorsMapping** per la tabella **Authors**.

```csharp
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");
```

Un oggetto **DataTableMapping** consente di usare in una classe **DataTable** nomi di colonne diversi da quelli presenti nel database. L'oggetto **DataAdapter** usa il mapping per mantenere la corrispondenza delle colonne quando la tabella viene aggiornata.

> [!NOTE]
> Se non si specifica un nome **TableName** o **DataTableMapping** quando si chiama il metodo **Fill** o **Update** di **DataAdapter**, **DataAdapter** cercherà un oggetto **DataTableMapping** denominato "Table". Il nome **TableName** di **DataTable** è "Table" se tale **DataTableMapping** non esiste. È possibile specificare un oggetto **DataTableMapping** predefinito creando un oggetto **DataTableMapping** con il nome "Table".

L'esempio di codice seguente crea un oggetto **DataTableMapping** (dallo spazio dei nomi <xref:System.Data.Common>) che viene impostato come mapping predefinito per la classe **DataAdapter** specificata denominandolo "Table". Viene quindi eseguito il mapping delle colonne della prima tabella nel set di risultati della query, ovvero la tabella **Customers** del database **Northwind**, a un set di nomi più semplici nella tabella **Northwind Customers** dell'oggetto <xref:System.Data.DataSet>. Per le colonne di cui non viene eseguito il mapping, viene usato il nome della colonna nell'origine dati.

[!code-csharp[SqlDataAdapter_TableMappings#1](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#1)]

In un contesto più avanzato, può essere necessario che lo stesso oggetto **DataAdapter** supporti il caricamento di diverse tabelle con mapping diversi. A tale scopo aggiungere altri oggetti **DataTableMapping**.

Quando al metodo **Fill** vengono passati un'istanza di **DataSet** e un nome di **DataTableMapping**, viene usato un mapping con tale nome, se esistente. In caso contrario, viene usata una classe **DataTable** con tale nome.

L'esempio seguente crea un oggetto **DataTableMapping** con il nome **Customers** e viene assegnato il nome **BizTalkSchema** a una classe **DataTable**. Viene quindi eseguito il mapping delle righe restituite dall'istruzione SELECT alla classe **DataTable** **BizTalkSchema**.

[!code-csharp[SqlDataAdapter_TableMappings#2](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#2)]

> [!NOTE]
> Se non viene indicato un nome di colonna di origine per il mapping di una colonna, verranno automaticamente generati nomi predefiniti. Al mapping della colonna viene assegnato il nome predefinito incrementale **SourceColumn** *N*, che inizia con **SourceColumn1**, se non viene indicato il nome della colonna di origine.

> [!NOTE]
> Se non viene indicato un nome di tabella di origine per il mapping di una tabella, verranno automaticamente generati nomi predefiniti. Al mapping della tabella viene assegnato il nome predefinito incrementale **SourceTable** *N*, che inizia con **SourceTable1**, se non viene indicato il nome della tabella di origine.

> [!NOTE]
> Si consiglia di evitare la convenzione di denominazione di **SourceColumn** *N* per il mapping di una colonna o di **SourceTable** *N* per il mapping di una tabella, perché il nome indicato può entrare in conflitto con il nome predefinito esistente del mapping di una colonna in **ColumnMappingCollection** o con il nome del mapping di una tabella in **DataTableMappingCollection**. Se il nome specificato esiste già, verrà generata un'eccezione.

## <a name="handle-multiple-result-sets"></a>Gestire più set di risultati

Se **SelectCommand** restituisce più tabelle, **Fill** genera automaticamente nomi di tabella con valori incrementali per le tabelle contenute in **DataSet**, che iniziano con il nome specificato e proseguono nel formato **TableName** *N*, che inizia con **TableName1**. È possibile eseguire il mapping del nome della tabella generato automaticamente al nome che si vuole specificare per la tabella in **DataSet**. Per un oggetto **SelectCommand** che restituisce le due tabelle **Customers** e **Orders**, ad esempio, si esegue la chiamata seguente a **Fill**.

```csharp
adapter.Fill(customersDataSet, "Customers");
```

Vengono create due tabelle in **DataSet**: **Customers** e **Customers1**. È possibile usare i mapping di tabelle per fare in modo che il nome della seconda tabella sia **Orders** invece di **Customers1**. A tale scopo, eseguire il mapping della tabella di origine di **Customers1** alla tabella **Orders** di **DataSet**, come illustrato nell'esempio seguente.

[!code-csharp[SqlDataAdapter_TableMappings#3](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#3)]

## <a name="see-also"></a>Vedere anche

- [DataAdapter e DataReader](dataadapters-datareaders.md)
- [Recupero e modifica di dati in ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
