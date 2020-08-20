---
description: Creazione, modifica ed eliminazione di indici spaziali
title: Creare, modificare ed eliminare indici spaziali | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4aeb545a92ef4eca7bdb7542b951021336de9800
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455449"
---
# <a name="create-modify-and-drop-spatial-indexes"></a>Creazione, modifica ed eliminazione di indici spaziali
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Un indice spaziale consente di eseguire in modo più efficiente determinate operazioni in una colonna con tipo di dati **geometry** o **geography** ( *colonna spaziale*). In una colonna spaziale è possibile specificare più di un indice spaziale. Ciò è utile, ad esempio, per indicizzare diversi parametri della suddivisione a mosaico in una sola colonna.  
  
 La creazione di indici spaziali è soggetta a un certo numero di limitazioni. Per altre informazioni, vedere [Restrizioni relative agli indici spaziali](#restrictions) .  
  
> [!NOTE]  
>  Per informazioni sulla relazione degli indici spaziali con la partizione e i filegroup, vedere la sezione "Osservazioni" in [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
##  <a name="creating-modifying-and-dropping-spatial-indexes"></a><a name="creating"></a> Creazione, modifica e rimozione di indici spaziali  
  
###  <a name="to-create-a-spatial-index"></a><a name="create"></a> Per creare un indice spaziale  
 **Per creare un indice spaziale tramite Transact-SQL**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **Per creare un indice spaziale tramite la finestra di dialogo Nuovo indice in Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>Per creare un indice spaziale in Management Studio  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, espandere il database che contiene la tabella con l'indice specificato e quindi espandere **Tabelle**.  
  
3.  Espandere la tabella per la quale si desidera creare l'indice.  
  
4.  Fare clic con il pulsante destro del mouse su **Indici** e scegliere **Nuovo indice**.  
  
5.  Nel campo **Nome indice** immettere un nome per l'indice.  
  
6.  Nell'elenco a discesa **Tipo di indice** selezionare **Spaziale**.  
  
7.  Per specificare la colonna spaziale che si vuole indicizzare, fare clic su **Aggiungi**.  
  
8.  Nella finestra di dialogo **Seleziona colonne da** *\<table name>* selezionare una colonna di tipo **geometry** o **geography** facendo clic sulla casella di controllo corrispondente. Le altre colonne spaziali eventualmente presenti diventano non modificabili. Se si desidera selezionare una colonna spaziale diversa, è innanzitutto necessario deselezionare la colonna attualmente selezionata. Al termine, fare clic su **OK**.  
  
9. Verificare la selezione della colonna nella griglia **Colonne chiave indice** .  
  
10. Nel riquadro **Selezione pagina** della finestra di dialogo **Proprietà indice** fare clic su **Spaziale**.  
  
11. Nella pagina **Spaziale** specificare i valori che si vogliono usare per le proprietà spaziali dell'indice.  
  
     Quando si crea un indice in una colonna di tipo **geometry** è necessario specificare le coordinate **(** _X-min_ **,** _Y-min_ **)** e **(** _X-max_ **,** _Y-max_ **)** del rettangolo di selezione. Per un indice in una colonna del tipo **geography** i campi del riquadro diventano di sola lettura dopo avere specificato lo schema a mosaico **Griglia geografica** , perché lo schema a mosaico della griglia geografica non usa un rettangolo di selezione.  
  
     È eventualmente possibile specificare valori non predefiniti per il campo **Celle per oggetto** e per la densità griglia a qualsiasi livello dello schema a mosaico. Il numero predefinito di celle per oggetto è 16 per [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o 8 per [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o versione successiva, mentre la densità della griglia predefinita è **Media** per [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
     È possibile selezionare GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID per lo schema a mosaico in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando si seleziona GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID, le opzioni Livello 1, Livello 2, Livello 3 e Livello 4 per la densità della griglia sono disabilitate.  
  
     Per altre informazioni su queste proprietà, vedere [Guida sensibile al contesto di Proprietà indice](../../relational-databases/indexes/index-properties-f1-help.md).  
  
12. Fare clic su **OK**.  
  
> [!NOTE]  
>  Per creare un altro indice spaziale nella stessa colonna spaziale o in una colonna diversa, ripetere i passaggi precedenti.  
  
  
 **Per creare un indice spaziale tramite Progettazione tabelle in Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>Per creare un indice spaziale in Progettazione tabelle  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella per la quale si vuole creare un indice spaziale e scegliere **Progetta**.  
  
     La tabella verrà visualizzata in Progettazione tabelle.  
  
2.  Selezionare una colonna **geometry** o **geography** per l'indice.  
  
3.  Scegliere **Indice spaziale** dal menu **Progettazione tabelle**.  
  
4.  Nella finestra di dialogo **Indici spaziali** fare clic su **Aggiungi**.  
  
5.  Selezionare il nuovo indice dall'elenco **Indice spaziale selezionato** e impostarne le proprietà nella griglia a destra. Per informazioni sulle proprietà, vedere [Finestra di dialogo Indici spaziali &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/4d84239a-68c7-4aa2-8602-2b51dd07260f).  
  
  
###  <a name="to-alter-a-spatial-index"></a><a name="alter"></a> Per modificare un indice spaziale  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  Per modificare opzioni specifiche di un indice spaziale, ad esempio BOUNDING_BOX o GRID, è possibile utilizzare un'istruzione CREATE SPATIAL INDEX che specifica DROP_EXISTING = ON oppure eliminare l'indice spaziale e crearne un nuovo. Per un esempio vedere [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
-   [Modificare un indice](../../relational-databases/indexes/modify-an-index.md)  
  
-   [Spostare un indice esistente in un filegroup diverso](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="to-drop-a-spatial-index"></a><a name="drop"></a> Per eliminare un indice spaziale  
 **Per eliminare un indice spaziale tramite Transact-SQL**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **Per eliminare un indice utilizzando Management Studio**  
 [Eliminare un indice](../../relational-databases/indexes/delete-an-index.md)  
  
 **Per eliminare un indice spaziale tramite Progettazione tabelle in Management Studio**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>Per eliminare un indice spaziale in Progettazione tabelle  
  
1.  In Esplora oggetti, selezionare con il pulsante destro del mouse la tabella contenente l'indice spaziale da eliminare, quindi selezionare **Progetta**.  
  
     La tabella verrà visualizzata in Progettazione tabelle.  
  
2.  Scegliere **Indice spaziale** dal menu **Progettazione tabelle**.  
  
     Verrà visualizzata la finestra di dialogo **Indice spaziale** .  
  
3.  Fare clic sull'indice da eliminare nella colonna **Indice spaziale selezionato** .  
  
4.  Fare clic su **Elimina**.  
  
  
##  <a name="restrictions-on-spatial-indexes"></a><a name="restrictions"></a> Restrizioni relative agli indici spaziali  
 Un indice spaziale può essere creato solo in una colonna di tipo **geometry** o **geography**.  
  
### <a name="table-and-view-restrictions"></a>Restrizioni per viste e tabelle  
 È possibile definire indici spaziali solo per una tabella con chiave primaria. Il numero massimo di colonne chiave primaria in una tabella è pari a 15.  
  
 La dimensione massima dei record di una chiave di indice è 895 byte. Dimensioni maggiori generano un errore.  
  
> [!NOTE]  
>  I metadati della chiave primaria non possono essere modificati se un indice spaziale è definito in una tabella.  
  
 Non è possibile specificare indici spaziali in viste indicizzate.  
  
### <a name="multiple-spatial-index-restrictions"></a>Restrizioni relative a più indici spaziali  
 È possibile creare fino a 249 indici spaziali in ognuna delle colonne spaziali in una tabella supportata. La creazione di più di un indice spaziale nella stessa colonna spaziale può essere utile, ad esempio, per indicizzare parametri della suddivisione a mosaico diversi in una sola colonna.  
  
 È possibile creare solo un indice spaziale alla volta.  
  
### <a name="spatial-indexes-and-process-parallelism"></a>Indici spaziali e parallelismo di processi  
 Per la compilazione di un indice è possibile utilizzare il parallelismo di processi disponibile.  
  
### <a name="version-restrictions"></a>Restrizioni della versione  
 Non è possibile eseguire la replica di schemi a mosaico spaziali introdotti in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. È necessario usare schemi a mosaico spaziali [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] per gli indici spaziali quando è necessario garantire la compatibilità con i database di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .  
  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
