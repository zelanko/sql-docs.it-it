---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33bdc74ffee071d8a5f9e7d10543bad133066b32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637063"
---
# <a name="mssqlserver_8710"></a>MSSQLSERVER_8710
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|MSSQLSERVER|  
|ID evento|8710|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Testo del messaggio|Le funzioni di aggregazione utilizzate con query CUBE, ROLLUP o GROUPING SET devono supportare l'unione di aggregazioni secondarie. Per risolvere il problema, rimuovere la funzione di aggregazione o scrivere la query utilizzando UNION ALL nelle clausole GROUP BY.|  
  
## <a name="explanation"></a>Spiegazione  
Una funzione di aggregazione è stata utilizzata con CUBE, ROLLUP o GROUPING SETS che non forniscono un metodo per unire aggregazioni secondarie.  
  
## <a name="user-action"></a>Azione dell'utente  
Per risolvere il problema, rimuovere la funzione di aggregazione o scrivere la query utilizzando UNION ALL nelle clausole GROUP BY.  
  
