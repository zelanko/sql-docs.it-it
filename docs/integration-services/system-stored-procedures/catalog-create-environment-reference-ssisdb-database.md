---
title: catalog.create_environment_reference (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 48069bea-31cb-4a0e-9849-a07edc94088f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73871d69a8fbdc56b2359aa888cbc08e572a6107
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65716913"
---
# <a name="catalogcreateenvironmentreference-ssisdb-database"></a>catalog.create_environment_reference (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Viene creato un riferimento all'ambiente per un progetto nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
catalog.create_environment_reference [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @environment_name = ] environment_name  
     , [ @reference_location = ] reference_location  
  [  , [ @environment_folder_name = ] environment_folder_name ]  
  [  , [ @reference_id = ] reference_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @folder_name = ] *folder_name*  
 Nome della cartella del progetto che fa riferimento all'ambiente. *folder_name* è di tipo **nvarchar(128)** .  
  
 [ @project_name = ] *project_name*  
 Nome del progetto che fa riferimento all'ambiente. *project_name* è di tipo **nvarchar(128)** .  
  
 [ @environment_name = ] *environment_name*  
 Nome dell'ambiente a cui viene fatto riferimento. *environment_name* è di tipo **nvarchar(128)** .  
  
 [ @reference_location = ] *reference_location*  
 Viene indicato se l'ambiente può essere individuato nella stessa cartella del progetto (riferimento relativo) o in una cartella diversa (riferimento assoluto). Utilizzare il valore `R` per indicare un riferimento relativo. Utilizzare il valore `A` per indicare un riferimento assoluto. *reference_location* è di tipo **char(1)** .  
  
 [ @environment_folder_name = ] *environment_folder_name*  
 Nome della cartella in cui si trova l'ambiente a cui viene fatto riferimento. Questo valore è richiesto per i riferimenti assoluti. *environment_folder_name* è di tipo **nvarchar(128)** .  
  
 [ @reference_id = ] *reference_id*  
 Viene restituito l'identificatore univoco per il nuovo riferimento. Questo parametro è facoltativo. *reference_id* è di tipo **bigint**.  
  
## <a name="return-code-value"></a>Valore del codice restituito  
 0 (esito positivo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa stored procedure è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazioni READ e MODIFY sul progetto e autorizzazione READ sull'ambiente  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errori e avvisi  
 Nell'elenco seguente vengono descritte alcune condizioni che possono generare un errore o un avviso:  
  
-   Nome della cartella non valido  
  
-   Nome del progetto non valido  
  
-   Utente senza autorizzazioni appropriate  
  
-   Un riferimento assoluto è specificato tramite il carattere `A` nel parametro *reference_location*, ma il nome della cartella non è stato specificato con il parametro *environment_folder_name*.  
  
## <a name="remarks"></a>Remarks  
 Un progetto può disporre di riferimenti all'ambiente relativi o assoluti. I riferimenti relativi fanno riferimento all'ambiente in base al nome. Per tali riferimenti è necessario che l'ambiente si trovi nella stessa cartella del progetto. I riferimenti assoluti fanno riferimento all'ambiente in base al nome e alla cartella e possono fare riferimento ad ambienti che si trovano in una cartella di destinazione diversa da quella del progetto. Un progetto può fare riferimento a più ambienti.  
  
  
