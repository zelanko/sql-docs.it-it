---
title: Supporto di SQL Server Integration Services per OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9dfaedb283f7b1dd6af08405f5229c994b8987a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111696"
---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>Supporto di SQL Server Integration Services per OLTP in memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile usare una tabella ottimizzata per la memoria, una vista che fa riferimento a tabelle ottimizzate per la memoria o una stored procedure compilata in modo nativo come origine o destinazione del pacchetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS). È possibile usare [ADO NET Source](../../integration-services/data-flow/ado-net-source.md), [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)o [ODBC Source](../../integration-services/data-flow/odbc-source.md) nel flusso di dati di un pacchetto SSIS e configurare il componente di origine per recuperare i dati da una tabella ottimizzata per la memoria o una vista oppure specificare un'istruzione SQL per eseguire una stored procedure compilata in modo nativo. Analogamente, è possibile usare [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md), [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)o [ODBC Destination](../../integration-services/data-flow/odbc-destination.md) per caricare i dati in una tabella ottimizzata per la memoria o una vista oppure specificare un'istruzione SQL per eseguire una stored procedure compilata in modo nativo.  
  
 È possibile configurare i componenti di origine e destinazione precedentemente citati in un pacchetto SSIS per le operazioni di lettura/scrittura nelle tabelle ottimizzate per la memoria e nelle viste nello stesso modo di altre tabelle e viste di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tuttavia, è necessario considerare gli aspetti importanti nella sezione seguente quando si utilizzano le stored procedure compilate in modo nativo.  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>Richiamare una stored procedure compilata in modo nativo da un pacchetto SSIS  
 Per richiamare una stored procedure compilata in modo nativo da un pacchetto SSIS, è consigliabile usare un'origine ODBC o una destinazione ODBC con un'istruzione SQL nel formato **\<nome stored procedure>** senza la parola chiave **EXEC**. Se si utilizza la parola chiave EXEC nell'istruzione SQL, verrà visualizzato un messaggio di errore perché la gestione connessione ODBC interpreta il testo del comando SQL come istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] anziché come una stored procedure e utilizza i cursori che non sono supportati per l'esecuzione di stored procedure compilate in modo nativo. La gestione connessione tratta l'istruzione SQL senza la parola chiave EXEC come chiamata di stored procedure e non utilizzerà un cursore.  
  
 È inoltre possibile utilizzare l'origine ADO.NET e l'origine OLE DB per chiamare una stored procedure compilata in modo nativo, ma è consigliabile utilizzare l'origine ODBC. Se si configura l'origine ADO.NET per eseguire una stored procedure compilata in modo nativo, verrà visualizzato un messaggio di errore perché il provider di dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient), utilizzato dall'origine ADO.NET per impostazione predefinita, non supporta l'esecuzione di una stored procedure compilata in modo nativo. È possibile configurare l'origine ADO.NET per utilizzare il provider di dati ODBC, il provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Tuttavia, si noti che le prestazioni dell'origine ODBC sono migliori di quelle dell'origine ADO.NET con il provider di dati ODBC.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto di SQL Server per OLTP in memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
