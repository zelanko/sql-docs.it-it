---
title: Connettersi a SQL Server o al database SQL di Azure
ms.custom: seo-lt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d489dac9355a573473063d1cafb32d42ed5fd98
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001997"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Connettersi a SQL Server o al database SQL di Azure

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Per usare server e database, è prima di tutto necessario connettersi al server. È possibile connettersi a più server contemporaneamente.

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) supporta diversi tipi di connessioni. Questo articolo fornisce dettagli per la connessione a SQL Server e al database SQL di Azure, ovvero per la connessione a un singolo database o a un pool elastico di Azure SQL. Per informazioni sulle altre opzioni di connessione, vedere i [collegamenti](#see-also) nella parte inferiore della pagina.
  
## <a name="connecting-to-a-server"></a>Connessione a un server  

1. In **Esplora oggetti** fare clic su **Connetti > Motore di database**.

   ![connessione](../media/connect-to-server/connect-db-engine.png)

1. Compilare il modulo **Connetti al server** e fare clic su **Connetti**:

   ![Connetti al server](../media/connect-to-server/connect.png)

1. Se ci si connette a un server di Azure SQL, è possibile che venga richiesto l'accesso per la creazione di una regola del firewall. Fare clic su **Accedi**. Se non viene visualizzata alcuna richiesta, procedere al Passaggio 6 più avanti.

   ![firewall](../media/connect-to-server/firewall-rule-sign-in.png)

1. Dopo l'accesso, il form viene precompilato con l'indirizzo IP specifico. Se l'indirizzo IP specifico viene modificato spesso, potrebbe risultare più facile concedere l'accesso a un intervallo. Selezionare quindi l'opzione più adatta al proprio ambiente. 

   ![firewall](../media/connect-to-server/new-firewall-rule.png)

1. Per creare la regola del firewall e connettersi al server fare clic su **OK**.

1. Il server viene visualizzato in **Esplora oggetti** dopo il completamento della connessione:

   ![connected](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Passaggi successivi

[Progettare, creare e aggiornare le tabelle](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Vedere anche

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[Scaricare SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Archiviazione di Azure](../f1-help/connect-to-microsoft-azure-storage.md)  
