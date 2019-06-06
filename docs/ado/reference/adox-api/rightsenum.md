---
title: RightsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RightsEnum
helpviewer_keywords:
- RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a34cbd8ee3d274d3b3d45049611ca9cc99fa7758
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718843"
---
# <a name="rightsenum"></a>RightsEnum
Specifica i diritti o le autorizzazioni per un gruppo o utente in un oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (&H4000)|L'utente o il gruppo dispone dell'autorizzazione per creare nuovi oggetti di questo tipo.|  
|**adRightDelete**|65536 (&H10000)|L'utente o il gruppo dispone dell'autorizzazione per eliminare i dati da un oggetto. Per gli oggetti, ad esempio **tabelle**, l'utente dispone dell'autorizzazione per eliminare i valori dei dati dai record.|  
|**adRightDrop**|256 (&H100)|L'utente o il gruppo dispone dell'autorizzazione per rimuovere gli oggetti dal catalogo. Ad esempio, **tabelle** può essere eliminato da un comando SQL DROP TABLE.|  
|**adRightExclusive**|512 (&H200)|L'utente o il gruppo dispone dell'autorizzazione per accedere all'oggetto in modo esclusivo.|  
|**adRightExecute**|536870912 (&H20000000)|L'utente o il gruppo dispone dell'autorizzazione per eseguire l'oggetto.|  
|**adRightFull**|268435456 (&H10000000)|L'utente o il gruppo ha tutte le autorizzazioni sull'oggetto.|  
|**adRightInsert**|32768 (&H8000)|L'utente o il gruppo dispone dell'autorizzazione per inserire l'oggetto. Per gli oggetti, ad esempio **tabelle**, l'utente dispone dell'autorizzazione per inserire dati nella tabella.|  
|**adRightMaximumAllowed**|33554432 (&H2000000)|L'utente o il gruppo è il numero massimo di autorizzazioni consentite dal provider. Autorizzazioni specifiche dipendono dal provider.|  
|**adRightNone**|0|L'utente o il gruppo non dispone di autorizzazioni per l'oggetto.|  
|**adRightRead**|-2147483648 (&H80000000)|L'utente o il gruppo dispone dell'autorizzazione per leggere l'oggetto. Per gli oggetti, ad esempio [tabelle](../../../ado/reference/adox-api/table-object-adox.md), l'utente dispone dell'autorizzazione per leggere i dati nella tabella.|  
|**adRightReadDesign**|1024 (&H400)|L'utente o il gruppo dispone dell'autorizzazione per leggere la struttura per l'oggetto.|  
|**adRightReadPermissions**|131072 (&H20000)|L'utente o gruppo possa visualizzare, ma non modificare, le autorizzazioni specifiche per un oggetto nel catalogo.|  
|**adRightReference**|8192 (&AMP; H2000)|L'utente o il gruppo dispone dell'autorizzazione per fare riferimento all'oggetto.|  
|**adRightUpdate**|1073741824 (&H40000000)|L'utente o il gruppo dispone dell'autorizzazione per aggiornare l'oggetto. Per gli oggetti, ad esempio **tabelle**, l'utente dispone dell'autorizzazione per aggiornare i dati nella tabella.|  
|**adRightWithGrant**|4096 (&H1000)|L'utente o il gruppo dispone dell'autorizzazione per concedere le autorizzazioni per l'oggetto.|  
|**adRightWriteDesign**|2048 (&H800)|L'utente o il gruppo dispone dell'autorizzazione per modificare la progettazione per l'oggetto.|  
|**adRightWriteOwner**|524288 (&H80000)|L'utente o il gruppo dispone dell'autorizzazione per modificare il proprietario dell'oggetto.|  
|**adRightWritePermissions**|262144 (&H40000)|L'utente o gruppo possa modificare le autorizzazioni specifiche per un oggetto nel catalogo.|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[Metodo SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
