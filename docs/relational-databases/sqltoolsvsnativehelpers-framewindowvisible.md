---
title: FrameWindowVisible | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 228238f4a326790f22f0298beb2e1b51fbfcf7d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126575"
---
# <a name="sqltoolsvsnativehelpers---framewindowvisible"></a>SqlToolsVSNativeHelpers - FrameWindowVisible
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Proprietà che specifica se una data cornice di finestra è visibile. Il metodo helper viene utilizzato dal codice gestito.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL WINAPI IsFrameWindowVisible(IVsWindowFrame* frame)  
{  
    if (NULL == frame)  
    {  
        return FALSE;  
    }  
  
    return S_OK == frame->IsVisible();  
}  
```  
  
#### <a name="parameters"></a>Parametri  
 *frame*  
  
 Puntatore IVsWindowFrame* a Visual Studio WindowFrame.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore booleano che specifica se la cornice della finestra specificata da *frame* è visibile.  
  
## <a name="see-also"></a>Vedere anche  
 [SqlToolsVSNativeHelpers](../relational-databases/sqltoolsvsnativehelpers.md)  
  
  
