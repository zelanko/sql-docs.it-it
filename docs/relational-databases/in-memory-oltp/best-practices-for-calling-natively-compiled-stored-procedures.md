---
title: Procedure consigliate - stored procedure compilate in modo nativo
description: Informazioni sulle procedure consigliate per le stored procedure compilate in modo nativo che in genere vengono usate nelle parti critiche per le prestazioni di un'applicazione.
ms.custom: seo-dt-2019
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f39fc1c7-cfec-4a95-97f6-6b95954694b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e26440be66b89ff789890169751a18500f465c00
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529372"
---
# <a name="best-practices-for-calling-natively-compiled-stored-procedures"></a>Procedure consigliate per chiamare stored procedure compilate in modo nativo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Le stored procedure compilate in modo nativo:  
  
-   Vengono in genere utilizzate nelle parti critiche per le prestazioni di un'applicazione.  
  
-   Vengono eseguite di frequente.  
  
-   È previsto che siano veloci.  
  
 Il vantaggio a livello di prestazioni garantito dall'utilizzo di una stored procedure compilata in modo nativo aumenta con il numero di righe e la quantità di logica elaborata dalla procedura. Ad esempio, tramite una stored procedure compilata in modo nativo vengono garantite prestazioni migliori se si usano uno o più dei componenti seguenti:  
  
-   Aggregazione.  
  
-   Join a cicli annidati.  
  
-   Operazioni di selezione, inserimento, aggiornamento ed eliminazione a più istruzioni.  
  
-   Espressioni complesse.  
  
-   Logica procedurale, ad esempio cicli e istruzioni condizionali.  
  
 Se è necessario elaborare una sola riga, l'utilizzo di una stored procedure compilata in modo nativo non può garantire un vantaggio in termini di prestazioni.  
  
 Per evitare che nel server debbano essere eseguiti il mapping dei nomi di parametro e la conversione dei tipi, assicurarsi di:  
  
-   Associare i tipi dei parametri passati alla stored procedure ai tipi nella definizione della stored procedure.  
  
-   Utilizzare i parametri ordinali (senza nome) per chiamare le stored procedure compilate in modo nativo. Per la massima efficienza di esecuzione, non usare parametri denominati.  
  
 Le inefficienze nei parametri con stored procedure compilate in modo nativo può essere rilevato tramite l'XEvent **natively_compiled_proc_slow_parameter_passing**:
 - Tipi non corrispondenti: **reason=parameter_conversion**
 - Parametri denominati: **reason=named_parameters**
 - Valori predefiniti: **reason=default** 
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure compilate in modo nativo](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
