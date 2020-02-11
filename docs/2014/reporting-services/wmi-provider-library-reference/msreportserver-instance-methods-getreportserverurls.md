---
title: Metodo GetReportServerUrls (MSReportServer_Instance WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f600d7bf2515cb77c587e5c9c3d5f8d1db1e343f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097192"
---
# <a name="getreportserverurls-method-wmi-msreportserver_instance"></a>Metodo GetReportServerUrls (MSReportServer_Instance WMI)
  Restituisce un elenco degli URL che è possibile utilizzare per accedere al server di report e alla gestione report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *ApplicationName []*  
 Matrice che contiene le applicazioni installate. I valori sono `ReportServerWebService` e `ReportManager`.  
  
 *URL []*  
 Matrice che contiene gli URL registrati correttamente.  
  
 *Length*  
 Valore intero che contiene la lunghezza delle matrici restituite.  
  
 *HRESULT*  
 Valore che indica l'esito positivo o un codice di errore.  
  
## <a name="return-values"></a>Valori restituiti  
  
## <a name="remarks"></a>Osservazioni  
 I metodi esposti dagli oggetti di gestione WMI vengono chiamati tramite la funzione InvokeMethod. Per altre informazioni, vedere gli argomenti relativi all'esecuzione di metodi in oggetti di gestione all'interno della documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:**[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
