---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdb3a128753ca5e6be23eadf1c0b4fb91e9654c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85674209"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esegue la manutenzione dello stato delle operazioni per il catalogo SSISDB.  
  
 La stored procedure corregge lo stato di eventuali pacchetti in esecuzione in caso di arresto dell'istanza del server [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 È possibile scegliere di abilitare la stored procedure per l'esecuzione automatica a ogni riavvio dell'istanza del server [!INCLUDE[ssIS](../../includes/ssis-md.md)], selezionando l'opzione **Abilita l'esecuzione automatica della stored procedure di Integration Services all'avvio di SQL Server** nella finestra di dialogo **Crea catalogo**.  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 nessuno  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ e MODIFY sull'istanza di esecuzione, autorizzazioni READ e EXECUTE sul progetto e, se applicabile, autorizzazioni per la lettura sull'ambiente a cui si fa riferimento  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
  
