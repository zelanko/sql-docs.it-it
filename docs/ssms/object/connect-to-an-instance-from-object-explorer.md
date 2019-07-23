---
title: Connettersi a SQL Server o al database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aeb46551b33f40ba6c42de705559e20d8c7b0315
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264606"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Connettersi a SQL Server o al database SQL di Azure

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Per usare server e database, è prima di tutto necessario connettersi al server. È possibile connettersi a più server contemporaneamente.

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) supporta diversi tipi di connessioni. Questo articolo fornisce dettagli per la connessione a SQL Server e al database SQL di Azure, ovvero per la connessione a un singolo database o a un pool elastico di Azure SQL. Per informazioni sulle altre opzioni di connessione, vedere i [collegamenti](#see-also) nella parte inferiore della pagina.
  
## <a name="connecting-to-a-server"></a>Connessione a un server  

1. In **Esplora oggetti** fare clic su **Connetti > Motore di database**.

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. Compilare il modulo **Connetti al server** e fare clic su **Connetti**:

   ![Connetti al server](../media/connect-to-server/connect.png)

1. Se ci si connette a un server di Azure SQL, è possibile che venga richiesto l'accesso per la creazione di una regola del firewall. Fare clic su **Accedi**. Se non viene visualizzata alcuna richiesta, procedere al Passaggio 6 più avanti.

   ![firewall](../media/connect-to-server/firewall-rule-sign-in.png)

1. Dopo l'accesso, il form viene precompilato con l'indirizzo IP specifico. Se l'indirizzo IP specifico viene modificato spesso, potrebbe risultare più facile concedere l'accesso a un intervallo. Selezionare quindi l'opzione più adatta al proprio ambiente. 

   ![firewall](../media/connect-to-server/new-firewall-rule.png)

1. Per creare la regola del firewall e connettersi al server fare clic su **OK**.

1. Il server viene visualizzato in **Esplora oggetti** dopo il completamento della connessione:

   ![Connessione completata](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Next Steps

[Progettare, creare e aggiornare le tabelle](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Vedere anche

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[Scaricare SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Archiviazione di Azure](../f1-help/connect-to-microsoft-azure-storage.md)  
