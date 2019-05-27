---
title: File di unit test di SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cee093c9-b97d-4fb0-b80f-806d071259dc
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9c595bd6d7cce21b9bf3428fadf772c4db4cdc07
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101915"
---
# <a name="sql-server-unit-test-files"></a>File di unit test di SQL Server
Analogamente agli unit test per il codice gestito, gli unit test di SQL Server si trovano nei progetti di test. È possibile visualizzare gli elementi che costituiscono uno unit test di SQL Server nella gerarchia di un progetto di test in **Esplora soluzioni**.  
  
Uno unit test di SQL Server è costituito da più elementi contenuti in diversi file. Nella tabella seguente vengono descritti i file che interagiscono per formare uno unit test di SQL Server.  
  
|**File**|**Descrizione**|  
|------------|-------------------|  
|cs o vb|Questo file di codice sorgente contiene una classe decorata con l'attributo [TestClass]. In questa classe è contenuto un singolo metodo di test per ognuno degli unit test di SQL Server contenuti. Questi metodi sono decorati con l'attributo [TestMethod].<br /><br />Ogni metodo di test contiene il codice appropriato per verificare il comportamento dello script di test Transact\-SQL. Questo codice viene generato quando si creano i metodi di test e può essere modificato.<br /><br />**NOTA:** se si fa doppio clic su questo file in **Esplora soluzioni**, la classe di test viene aperta nella finestra di progettazione unit test di SQL Server. Per aprire il file con estensione cs o vb e visualizzare il relativo codice sorgente, fare clic con il pulsante destro del mouse sul file in **Esplora soluzioni** e quindi scegliere **Visualizza codice**.|  
|resx|Questo file di risorse contiene gli script Transact\-SQL per tutti i test nel file con estensione cs o vb associato. Questo gruppo di script include gli script di pre-test, test e post-test. Il file di risorse contiene il codice XML che è possibile modificare. Il file di risorse viene compilato nell'assembly di test.<br /><br />È consigliabile creare il codice degli script Transact\-SQL tramite la **finestra di progettazione unit test di SQL Server**. Per altre informazioni sugli script usati negli unit test di SQL Server, vedere [Script in unit test di SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|app.config|In questo file vengono archiviate le stringhe di connessione al database per il progetto di test, oltre ad altre impostazioni di configurazione di unit test di SQL Server, ad esempio il timeout del comando. Per altre informazioni, vedere [Script in unit test di SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).|  
|SQLDatabaseSetup.cs o SQLDatabaseSetup.vb|Questo file contiene una classe che prepara l'ambiente di test per tutti gli unit test di SQL Server nel progetto di test. In base alle impostazioni di configurazione nel file app.config è possibile distribuire un progetto di database di SQL Server nel database di test.|  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e definizione di unit test di SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Creazione e definizione di unit test di SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Verifica del codice di database tramite unit test di SQL Server](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[Script in unit test di SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
  
