---
title: Esecuzione di Stored procedure (OLE DB) | Microsoft Docs
description: Esecuzione di stored procedure (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- OLE DB Driver for SQL Server, stored procedures
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 0059c7c6e03c9abb9edf4cb3db35f8435174d8fc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795895"
---
# <a name="stored-procedures---running"></a>Stored procedure - Esecuzione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Durante l'esecuzione di istruzioni, la chiamata a una stored procedure nell'origine dati, in alternativa all'esecuzione o alla preparazione diretta di un'istruzione nell'applicazione client, può offrire i vantaggi seguenti:  
  
-   Prestazioni più elevate.  
  
-   Overhead di rete ridotto.  
  
-   Maggiore consistenza.  
  
-   Maggiore precisione.  
  
-   Maggior numero di funzionalità.  
  
 Il Driver OLE DB per SQL Server supporta tre dei meccanismi che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usano stored procedure per restituire i dati:  
  
-   Ogni istruzione SELECT nella procedura genera un set di risultati.  
  
-   La procedura può restituire dati tramite parametri di output.  
  
-   La procedura può avere un codice restituito di tipo integer.  
  
 L'applicazione deve essere in grado di gestire tutti questi output dalle stored procedure.  
  
 Provider OLE DB diversi restituiscono parametri di output e valori in momenti diversi durante l'elaborazione dei risultati. Nel caso del driver OLE DB per SQL Server i parametri di output e i codici restituiti non vengono specificati finché il consumer non ha recuperato o annullato i set di risultati restituiti dalla stored procedure. I codici e i parametri di output vengono restituiti nell'ultimo pacchetto TDS dal server.  
  
 I provider utilizzano la proprietà DBPROP_OUTPUTPARAMETERAVAILABILITY per segnalare la restituzione di parametri di output e valori. Questa proprietà è inclusa nel set di proprietà DBPROPSET_DATASOURCEINFO.  
  
 Il driver OLE DB per SQL Server imposta la proprietà DBPROP_OUTPUTPARAMETERAVAILABILITY su DBPROPVAL_OA_ATROWRELEASE per indicare che i codici e i parametri di output non vengono restituiti finché il set di risultati non viene elaborato o rilasciato.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure](../../oledb/ole-db/stored-procedures.md)  
  
  
