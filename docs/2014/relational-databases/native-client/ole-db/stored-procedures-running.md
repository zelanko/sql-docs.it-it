---
title: Esecuzione di stored procedure (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 91d6da9e7d9fd17d35d9868834c6b0d688519ff7
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704174"
---
# <a name="running-stored-procedures-ole-db"></a>Esecuzione di stored procedure (OLE DB)
  Durante l'esecuzione di istruzioni, la chiamata a una stored procedure nell'origine dati, in alternativa all'esecuzione o alla preparazione diretta di un'istruzione nell'applicazione client, può offrire i vantaggi seguenti:  
  
-   Prestazioni più elevate.  
  
-   Overhead di rete ridotto.  
  
-   Maggiore consistenza.  
  
-   Maggiore precisione.  
  
-   Maggior numero di funzionalità.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta tre dei meccanismi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzati dalle stored procedure per restituire i dati:  
  
-   Ogni istruzione SELECT nella procedura genera un set di risultati.  
  
-   La procedura può restituire dati tramite parametri di output.  
  
-   La procedura può avere un codice restituito di tipo integer.  
  
 L'applicazione deve essere in grado di gestire tutti questi output dalle stored procedure.  
  
 Provider OLE DB diversi restituiscono parametri di output e valori in momenti diversi durante l'elaborazione dei risultati. Nel caso del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native client, i parametri di output e i codici restituiti non vengono forniti fino a quando il consumer non ha recuperato o annullato i set di risultati restituiti dall'stored procedure. I codici e i parametri di output vengono restituiti nell'ultimo pacchetto TDS dal server.  
  
 I provider utilizzano la proprietà DBPROP_OUTPUTPARAMETERAVAILABILITY per segnalare la restituzione di parametri di output e valori. Questa proprietà è inclusa nel set di proprietà DBPROPSET_DATASOURCEINFO.  
  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client imposta la proprietà DBPROP_OUTPUTPARAMETERAVAILABILITY su DBPROPVAL_OA_ATROWRELEASE per indicare che i codici restituiti e i parametri di output non vengono restituiti finché il set di risultati non viene elaborato o rilasciato.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure](stored-procedures.md)  
  
  
