---
title: Risoluzione dei problemi relativi a unit test del database di SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cf4c9cd1-7e73-4c3b-922a-68b9247e7b33
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b7203572d01ca9f344b96a7008dd78b2e35bcdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110616"
---
# <a name="troubleshooting-sql-server-database-unit-testing-issues"></a>Risoluzione dei problemi relativi a unit test del database di SQL Server
Quando si eseguono unit test di SQL Server è possibile che si verifichino i problemi descritti in questo argomento:  
  
-   [Modifiche a unit test e App.Config ignorate quando si eseguono unit test](#UnitTestingAndAppConfigChanges)  
  
-   [Distribuzione del database a una destinazione imprevista quando si eseguono unit test](#DatabaseDeploymentInUnitTests)  
  
-   [Timeout quando si eseguono unit test di database](#TimeoutsDuringUnitTests)  
  
## <a name="UnitTestingAndAppConfigChanges"></a>Modifiche a unit test e App.Config ignorate quando si eseguono unit test  
Se si modifica il file App.Config nel progetto di test, è necessario ricompilare tale progetto prima che le modifiche abbiano effetto. Queste modifiche includono quelle apportate al file App.Config usando la finestra di dialogo **Configurazione di test di SQL Server**. Se il progetto di test non viene ricompilato, le modifiche non verranno applicate quando si eseguono gli unit test.  
  
## <a name="DatabaseDeploymentInUnitTests"></a>Distribuzione del database a una destinazione imprevista quando si eseguono unit test  
Se si distribuisce un database da un progetto di database quando si eseguono gli unit test, il database verrà distribuito utilizzando le informazioni sulla stringa di connessione specificate nella configurazione degli unit test. Le informazioni sulla connessione specificate nelle proprietà di debug del progetto di database non vengono usate per questa attività, quindi è possibile eseguire unit test di SQL Server su istanze diverse dello stesso database.  
  
## <a name="TimeoutsDuringUnitTests"></a>Timeout quando si eseguono unit test di database  
Se gli unit test del database non riescono a causa di un timeout, è possibile aumentare il periodo di timeout aggiornando il file app.config nel progetto di test. Il timeout della connessione, definito nella stringa di connessione, specifica il periodo di attesa per la connessione al server dello unit test. Il timeout del comando, che deve essere definito direttamente nel file app.config, specifica il periodo di attesa per l'esecuzione dello script Transact\-SQL da parte dello unit test. In caso di problemi con gli unit test a esecuzione prolungata, provare ad aumentare il valore di timeout del comando nell'elemento di contesto appropriato. Ad esempio, per specificare un timeout del comando di 120 secondi per l'elemento **PrivilegedContext**, aggiornare il file app.config come segue:  
  
```  
<SqlUnitTesting_VS2010>  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\..\..\..\Visual Studio 2010\Projects\Database10\Database10\AdventureWorks.sqlproj"  
        Configuration="Debug" />  
    <DataGeneration ClearDatabase="true" />  
    <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="30" />  
    <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="120" />  
</SqlUnitTesting_VS2010>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Creare unit test di SQL Server per funzioni, trigger e stored procedure](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[Procedura: Configurare l'esecuzione di unit test di SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
