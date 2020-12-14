---
title: Aggiungere vincoli esistenti a un DataSet
description: Descrive come aggiungere vincoli esistenti a una classe DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 9471f62c36604cb01ea78f558ac3bfbcb7f4bc01
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772271"
---
# <a name="add-existing-constraints-to-a-dataset"></a>Aggiungere vincoli esistenti a un DataSet

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Il metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A> di <xref:Microsoft.Data.SqlClient.SqlDataAdapter> compila una classe <xref:System.Data.DataSet> solo con colonne e righe di tabella di un'origine dati. Anche se i vincoli vengono in genere impostati dall'origine dati, per impostazione predefinita il metodo **Fill** non aggiunge queste informazioni sullo schema alla classe **DataSet**.

Per popolare **DataSet** con le informazioni esistenti sui vincoli della chiave primaria da un'origine dati, è possibile chiamare il metodo <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> di **DataAdapter** oppure impostare la proprietà <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> di **DataAdapter** su **AddWithKey** prima di chiamare **Fill**. Ciò garantisce che i vincoli della chiave primaria in **DataSet** riflettano quelli nell'origine dati.

> [!NOTE]
> Le informazioni sul vincolo di chiave esterna non sono incluse e devono essere create in modo esplicito.

L'aggiunta delle informazioni sullo schema in una classe **DataSet** prima di compilarla con i dati assicura che i vincoli della chiave primaria siano inclusi con gli oggetti <xref:System.Data.DataTable> in **DataSet**. In questo modo, quando vengono effettuate altre chiamate per compilare **DataSet**, le informazioni nella colonna della chiave primaria vengono usate per confrontare le nuove righe provenienti dall'origine dati con le righe correnti in ogni **DataTable** e i dati correnti nelle tabelle vengono sovrascritti con i dati provenienti dall'origine dati. Senza le informazioni sullo schema, le nuove righe provenienti dall'origine dati verrebbero aggiunte a **DataSet** generando righe duplicate.

> [!NOTE]
> Se una colonna in un'origine dati viene identificata come colonna con incremento automatico, il metodo <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> o il metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A> con la proprietà <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> impostata su **AddWithKey** crea un oggetto **DataColumn** con una proprietà **AutoIncrement** impostata su `true`. È tuttavia necessario impostare direttamente i valori di **AutoIncrementStep** e **AutoIncrementSeed**.

> [!NOTE]
> Se si usa **FillSchema** o si imposta **MissingSchemaAction** su **AddWithKey**, è necessaria un'elaborazione aggiuntiva nell'origine dati per determinare le informazioni della colonna della chiave primaria. Questa ulteriore elaborazione può ridurre le prestazioni. Se le informazioni sulla chiave primaria sono note in fase di progettazione, è consigliabile specificare la colonna o le colonne della chiave primaria in modo esplicito per migliorare le prestazioni.

L'esempio di codice seguente descrive come aggiungere le informazioni sullo schema a **DataSet** usando <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

L'esempio di codice seguente descrive come aggiungere le informazioni sullo schema a **DataSet** usando la proprietà <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> e il metodo <xref:System.Data.Common.DbDataAdapter.Fill%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="handling-multiple-result-sets"></a>Gestione di più set di risultati

Se l'oggetto **DataAdapter** rileva più set di risultati restituiti da <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, verranno create più tabelle in **DataSet**. Alle tabelle viene assegnato un nome predefinito incrementale in base zero **Table** *N*, che inizia con **Table** invece che con "Table0". Alle tabelle verrà assegnato il nome incrementale in base zero **TableName** *N*, che inizia con **TableName** invece che con "TableName0" se il nome di una tabella viene passato come argomento al metodo <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>.

## <a name="see-also"></a>Vedere anche

- [DataAdapter e DataReader](dataadapters-datareaders.md)
- [Recupero e modifica di dati in ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET per SQL Server](microsoft-ado-net-sql-server.md)
